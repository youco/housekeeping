# Colab

## matplotで日本語を表示する

```python
!pip install japanize-matplotlib

import matplotlib.pyplot as plt
import japanize_matplotlib

plt.plot([1, 2, 3, 4])
plt.xlabel('簡単なグラフ')
plt.show()
```

## Pandasの表示制限を解除する

```python
#カラム内の文字数。デフォルトは50だった
pd.set_option("display.max_colwidth", 80)
#行数
pd.set_option("display.max_rows", 101)
```

