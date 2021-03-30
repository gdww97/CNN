# 1.LeNet5

  1994年，LeCun提出，论文地址[Gradient-based learning applied to document recognition](https://ieeexplore.ieee.org/document/726791?reload=true&arnumber=726791)

![](..\figures\图1 LeNet5.png)

<center>图1 LeNet5网络结构<center>

  pytorch实现

```python
class LeNet5(nn.Module):
    def __init__(self):
        self.conv1 = nn.Conv2d(1, 6, 5, 1, 0)
        self.maxpool1 = nn.MaxPool2d(2, 2)
        self.conv2 = nn.Conv2d(5, 16, 5, 1, 0)
        self.maxpool2 = nn.MaxPool2d(2, 2)
        self.conv3 = nn.Conv2d(16, 120, 5, 1, 0)
        self.fc1 = nn.Linear(120, 84)
        self.fc2 = nn.Linear(84, 10)
    
    def forward(self, x):
        x = self.conv1(x)
        x = self.maxpool1(x)
        x = self.conv2(x)
        x = self.maxpool2(x)
        x = self.conv3(x)
        x = torch.flatten(x, 1)
        x = self.fc1(x)
        x = self.fc2(x)
        return x
```