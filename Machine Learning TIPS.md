# Machine Learning TIPS

## sklearn

### StandardScaler

#### Usage

```python
from sklearn.preprocessing import StandardScaler
data = # example
scaler = StandardScaler()
scaler.fit(data)
scaled_data = scaler.transform(data)
```

See [scikit-learn 0.19.2 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html) for more infomation.