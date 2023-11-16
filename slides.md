---
theme: seriph
background: ./Cheetah.jpg
class: text-center
lineNumbers: false
drawings:
  persist: false
transition: fade
title: BenchmarkDotNet
mdc: true
hideInToc: true
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

# Demo

## 1. Install Template

```
dotnet new install BenchmarkDotNet.Templates
```

## 2. Configure BenchmarkDotNet

```csharp

[MemoryDiagnoser]
[Benchmark(Baseline = true)]
[Params(1,4...)
```

## 3. Execute in Release Mode from Command Line

## 4. Study Results

---

# Q&A