---
theme: Seriph
background: Cheetah.jpg
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

* What are these?
* What are they used for?
* Can BenchmarkDotNet be Used for API Performance or Load Testing?

---

# Before You Dive Into Micro Benchmarks

* Motivation
* Identifiyig the hot path
* Stop waches
* Profilers
* Micro Benchmark = Testing isolated scenariosr

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