---
Created by: Shudipto Trafder
Created time: 2024-04-24T14:44
Last edited by: Shudipto Trafder
Last edited time: 2024-04-24T14:51
tags:
  - Statistics
---
#### 1. Mean
The **mean**, often referred to as the **average**, is the sum of all values in a dataset divided by the number of values. It provides a central value for the data.

**Formula:**
$\text{Mean} (\mu) = \frac{1}{N} \sum_{i=1}^{N} x_i ]$

Where:
- ( N ) = number of observations
- ( x_i) = each individual observation

**Example:**
For the dataset [2, 4, 6, 8, 10]:
$[ \text{Mean} = \frac{2 + 4 + 6 + 8 + 10}{5} = 6 ]$

#### 2. Median
The **median** is the middle value in a dataset when the values are arranged in ascending or descending order. If the dataset has an even number of observations, the median is the average of the two middle values.

**Steps to find the Median:**
1. Arrange the data in ascending order.
2. If the number of observations $(( N ))$ is odd, the median is the middle value.
3. If \( N \) is even, the median is the average of the two middle values.

**Example:**
For the dataset [2, 4, 6, 8, 10] (odd number of observations):
- Median = 6

For the dataset [2, 4, 6, 8] (even number of observations):
$Median = (\frac{4 + 6}{2} = 5)$

#### 3. Mode
The **mode** is the value that appears most frequently in a dataset. A dataset may have one mode, more than one mode, or no mode at all if no value repeats.

**Example:**
For the dataset [1, 2, 2, 3, 4]:
- Mode = 2 (since 2 appears twice)

For the dataset [1, 1, 2, 2, 3, 3]:
- Modes = 1, 2, 3 (all appear twice)

#### 4. Variance
**Variance** is a measure of how much the values in a dataset deviate from the mean. It is the average of the squared differences from the mean. Variance provides an idea of the data's spread or dispersion.

**Formula:**
$[ \text{Variance} (\sigma^2) = \frac{1}{N} \sum_{i=1}^{N} (x_i - \mu)^2 ]$

Where:
- \( N \) = number of observations
- $( x_i )$ = each individual observation
- $( \mu )$ = mean of the dataset

**Steps to Calculate Variance:**
1. Calculate the mean $( \mu )$ of the dataset.
2. Subtract the mean from each observation to find the deviation.
3. Square each deviation.
4. Sum all the squared deviations.
5. Divide the sum by the number of observations (\( N \)).

**Example:**
For the dataset [2, 4, 6, 8, 10]:

1. Calculate the mean $(( \mu ))$:
$[ \mu = 6 ]$

2. Calculate each deviation from the mean and square it:
$$
[ (2-6)^2 = 16 ]
[ (4-6)^2 = 4 ]
[ (6-6)^2 = 0 ]
[ (8-6)^2 = 4 ]
[ (10-6)^2 = 16 ]
$$
3. Sum the squared deviations:
$[ 16 + 4 + 0 + 4 + 16 = 40 ]$

4. Divide by the number of observations (\( N = 5 \)):
$[ \sigma^2 = \frac{40}{5} = 8 ]$

**Summary:**
- Variance is the average of the squared deviations from the mean.
- It provides a measure of the spread of the data points.

**Relationship to Standard Deviation:**
The standard deviation is the square root of the variance:
$[ \sigma = \sqrt{\sigma^2} ]$

In the example above:
$[ \sigma = \sqrt{8} \approx 2.83 ]$

#### 5. Standard Deviation
The **standard deviation** measures the amount of variation or dispersion in a dataset. A low standard deviation indicates that the values tend to be close to the mean, while a high standard deviation indicates that the values are spread out over a wider range.

**Formula:**
$[ \text{Standard Deviation} (\sigma) = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (x_i - \mu)^2} ]$
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mtext>Standard&nbsp;Deviation&nbsp;(</mtext><mi>σ</mi><mtext>)</mtext><mo>=</mo><msqrt><mtext>Variance</mtext></msqrt></mrow><annotation encoding="application/x-tex">\text{Standard Deviation (}\sigma\text{)} = \sqrt{\text{Variance}}
</annotation></semantics></math>

Where:
- $( N )$ = number of observations
- $( x_i )$ = each individual observation
- $( \mu )$ = mean of the dataset

**Example:**
For the dataset [2, 4, 6, 8, 10]:

1. Calculate the mean $( \mu )$:
$[ \mu = 6 ]$

2. Calculate each deviation from the mean, square it, and sum them up:
$[ (2-6)^2 + (4-6)^2 + (6-6)^2 + (8-6)^2 + (10-6)^2 = 16 + 4 + 0 + 4 + 16 = 40 ]$

3. Divide by the number of observations (N = 5) and take the square root:
$[ \sigma = \sqrt{\frac{40}{5}} = \sqrt{8} \approx 2.83 ]$

