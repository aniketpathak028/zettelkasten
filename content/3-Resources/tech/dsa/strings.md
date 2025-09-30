## Strings


```python
# s = "1234567891011121314...." find the nth digit

def find_nth_digit(n):
    if n < 10:
        return n

    digit_length = 1
    count = 9
    start = 1

    while n > digit_length * count:
        n -= digit_length * count
        digit_length += 1
        count *= 10
        start *= 10

    start += (n - 1) // digit_length
    num_str = str(start)
    return int(num_str[(n - 1) % digit_length])

print(find_nth_digit(11))  # Example usage, should return 0
print(find_nth_digit(501))  # Example usage, should return 1
```

    0
    3

