# Performance Degradation After Upgrading to .NET 8..? ..What?

I want to share with you some interesting insights I gained from upgrading a data-intensive service that I work on. This service handles large amounts of data in lists and arrays and has some complex logic that loops through these data structures.

I decided to upgrade the service from .NET 7 to .NET 8, which was released a few weeks ago (November 14, 2023). The upgrade process was smooth and easy. However, when I ran a load test on the Azure Container Apps platform, I noticed that the performance of the upgraded service was worse than the previous version. This puzzled me and made me curious to find out what was causing this issue.

I wrote a code to compare the performance of different looping constructs in C#. To do that, I created an integer array and filled it with random numbers. Then, I used various loops such as for, foreach, while, and do-while to iterate over the array and calculate the sum of its elements. I repeated this process for arrays of different sizes: 100, 1000, 10,000, and 100,000 items. I also ran the same code on both .NET 7 and .NET 8 to see if there was any difference in speed or memory usage. 

## .NET 7 Results 
<br>

![.NET 7 benchmark summary](https://media.licdn.com/dms/image/v2/D5612AQHZ6l7m0L0NGw/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1704512144929?e=1751500800&v=beta&t=MApcqjuZG0dJWGL3ky8GgqNhry__7WbH1eORA2cYWfQ)

## .NET 8 Results
<br>

![.NET 8 benchmark summary](https://media.licdn.com/dms/image/v2/D5612AQGEY5Q7nIoOOw/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1704512079500?e=1751500800&v=beta&t=M-0BGABHgBlJ5H_-Eta17TZJYWenLERCiLA2G1Hu9h0)

---

## Legends
- **Size:** Value of the 'Size' parameter 
- **Mean:** Arithmetic mean of all measurements 
- **Error:** Half of 99.9% confidence interval 
- **StdDev:** Standard deviation of all measurements 
- **Median:** Value separating the higher half of all measurements (50th percentile) 
- **Ratio:** Mean of the ratio distribution ([Current]/[Baseline]) 
- **RatioSD:** Standard deviation of the ratio distribution ([Current]/[Baseline]) 
- **Allocated:** Allocated memory per single operation (managed only, inclusive, 1KB = 1024B)
- **Alloc Ratio:** Allocated memory ratio distribution ([Current]/[Baseline]) 
- **1 ns:** 1 Nanosecond (0.000000001 sec)

If you are interested, here is [the code I wrote](https://github.com/gayanishakaraw/loop-benchmark/). Feel free to try it out. 

For now, I'm sticking with .NET 7 for my services until I see some improvement in the performance of .NET 8.
This is not meant to discourage you from using .NET 8. I'm a big fan of the new features that come with .NET 8 and C# 12. I just wanted to share my findings with you and help you understand how to measure and compare the speed of loops. 
I hope this will be useful for you and your projects.

Cheers!
