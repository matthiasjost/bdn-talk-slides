---
theme: seriph
background: /cheetah.jpg
class: text-center
lineNumbers: false
drawings:
  persist: false
transition: fade
title: BenchmarkDotNet
mdc: true
hideInToc: true
highlighter: shiki
---



---
class: text-center
layout: cover
background: none
hideInToc: true
---

# BenchmarkDotNet


---
hideInToc: true
---

# Table of contents

<Toc maxDepth="1"></Toc>

---r
hideInToc: false
---

# Micro Benchmarks
## What are these?
Micro = Testing code pieces

## What are they used for?
Comparing scenarios (memory and performance)

## What about APIs (Load and Stress Testing)?
  * JMeter
  * NBomber
  * (BenchmarkDotNet)


---

# Before We Start

## 🔥 Identifiyig the Hot Path First
## ⏱️ Stop Watches
## 🕵️ Profilers
## 🔬 Micro Benchmarks = Testing Isolated Scenarios

---

# Template and NuGet

## Optional Template 
```
dotnet new install BenchmarkDotNet.Templates
```

![Local Image](/screenshot-project-template.png)

## NuGet
```
PM> NuGet\Install-Package BenchmarkDotNet
```


---


# Step-by Step

## 1. Project Setup

## 2. Write Scenarios and Verify!

## 3. Configure BenchmarkDotNet

```csharp
[MemoryDiagnoser]
[Benchmark(Baseline = true)]
[Params(1,4...)
```

## 

## 4. Execute in Release Mode from Command Line

## 5. Study Results


---

# Program.cs

```csharp {all|9,10|12,13|all}
using BenchmarkDotNet.Configs;
using BenchmarkDotNet.Running;
 
namespace BenchmarkSuite5;
public class Program
{
  public static void Main(string[] args)
  {
    var config = DefaultConfig.Instance;
    var summary = BenchmarkRunner.Run<Benchmarks>(config, args);
 
    // Use this to select benchmarks from the console:
    // var summaries = BenchmarkSwitcher.FromAssembly(typeof(Program).Assembly).Run(args, config);
  }
}
```
---

# Benchmark.cs


```csharp {all|8,9,10,11,12r|all}
using BenchmarkDotNet;
using BenchmarkDotNet.Attributes;
using System;

namespace BenchmarkSuite5;
public class Benchmarks
{
  [Benchmark]
  public void Scenario1()
  {
    // Implement your benchmark here
  }

  [Benchmark]
  public void Scenario2()
  {
    // Implement your benchmark here
  }
}
```

---

# Running Benchmarks

* Do execute from the command line!

```
dotnet run -c Release
```

![Local Image](/screenshot-project-build.png)

* BDN executes your benchmark methods multiple times
* Goal: Steady and reliable results

---

# Understanding the Results

```
BenchmarkDotNet=v0.13.4, OS=Windows 11 (10.0.22635.2771)
11th Gen Intel Core i7-1165G7 2.80GHz, 1 CPU, 8 logical and 4 physical cores
 
|                           Method |      Job |  Runtime |        Mean |       Error |      StdDev |  Ratio | RatioSD |
|--------------------------------- |--------- |--------- |------------:|------------:|------------:|-------:|--------:|
|      FirstOrDefault_Indexed_Last | .NET 8.0 | .NET 8.0 |    479.3 us |    30.31 us |    89.36 us |   0.96 |    0.26 |
|     FirstOrDefault_Indexed_First | .NET 8.0 | .NET 8.0 |    493.3 us |    35.22 us |   103.85 us |   0.99 |    0.32 |
|     SingleOrDefault_Indexed_Last | .NET 8.0 | .NET 8.0 |    517.7 us |    30.65 us |    89.41 us |   1.00 |    0.00 |
|    SingleOrDefault_Indexed_First | .NET 8.0 | .NET 8.0 |    486.5 us |    35.18 us |   103.73 us |   0.96 |    0.26 |
|   FirstOrDefault_NotIndexed_Last | .NET 8.0 | .NET 8.0 | 51,649.6 us | 2,765.84 us | 7,980.08 us | 103.08 |   23.39 |
|  FirstOrDefault_NotIndexed_First | .NET 8.0 | .NET 8.0 | 19,363.5 us |   871.89 us | 2,570.80 us |  38.67 |    8.99 |
|  SingleOrDefault_NotIndexed_Last | .NET 8.0 | .NET 8.0 | 52,017.6 us | 2,065.92 us | 5,927.50 us | 104.34 |   24.74 |
| SingleOrDefault_NotIndexed_First | .NET 8.0 | .NET 8.0 | 54,610.0 us | 2,435.62 us | 7,066.18 us | 108.64 |   23.25 |
```

---

# Useful Attributes


```csharp
[MemoryDiagnoser]
[Params(1,4...)
[SimpleJob(RuntimeMoniker.Net70)]
[SimpleJob(RuntimeMoniker.Net80)]
[ReturnValueValidator(failOnError: true)]
```

---

# Validating Results

```csharp
[ReturnValueValidator(failOnError: true)]
```

- Unit tests!

---

# Q&A