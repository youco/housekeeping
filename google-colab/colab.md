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

