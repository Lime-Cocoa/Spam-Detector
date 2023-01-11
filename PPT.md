---
marp: true
header: '自然语言处理'
---
<!-- paginate: true -->
# 基于Scikit-learn的垃圾短信检测器

---
## Scikit-learn简介

---
Scikit-learn是一个用于机器学习的开源 的Python的库。它包含了许多机器学习算法和工具，可以用来解决各种机器学习问题，例如分类、回归、聚类、降维、模型评估和模型选择等。

---
## 基本步骤

---
1. 收集数据并且分类
2. 将数据集划分为训练集和测试集
3. 寻找合适的分类器和矢量化器
4. 用训练集拟合每一个分类器并且使用测试集来计算准确率
5. 找到精度最高的分类器和矢量器组合

---
### 收集数据并且分类

---
在[kaggle](https://www.kaggle.com/datasets/uciml/sms-spam-collection-dataset)上有一个类似的题目，我们就直接使用它的数据集了。

---
![kMokw.png](https://i.328888.xyz/2023/01/08/kMokw.png)

---
### 将数据集划分为训练集和测试集

---
```Python
train_data = data[:4400] # 4400 items
test_data = data[4400:] # 1172 items
```

---
### 寻找合适的分类器和矢量化器

---
分类器种类
```Python
    BernoulliNB(),
    RandomForestClassifier(n_estimators=100, n_jobs=-1),
    AdaBoostClassifier(),
    BaggingClassifier(),
    ExtraTreesClassifier(),
    GradientBoostingClassifier(),
    DecisionTreeClassifier(),
    CalibratedClassifierCV(),
    DummyClassifier(),
    PassiveAggressiveClassifier(),
    RidgeClassifier(),
    RidgeClassifierCV(),
    SGDClassifier(),
    OneVsRestClassifier(SVC(kernel='linear')),
    OneVsRestClassifier(LogisticRegression()),
    KNeighborsClassifier()
```

---
矢量器种类
```Python
    CountVectorizer(),
    TfidfVectorizer(),
    HashingVectorizer()
```

---
### 用训练集拟合每一个分类器并且使用测试及来计算准确率

---
```Python
perform(
    [
        BernoulliNB(),
        RandomForestClassifier(n_estimators=100, n_jobs=-1),
        AdaBoostClassifier(),
        BaggingClassifier(),
        ExtraTreesClassifier(),
        GradientBoostingClassifier(),
        DecisionTreeClassifier(),
        CalibratedClassifierCV(),
        DummyClassifier(),
        PassiveAggressiveClassifier(),
        RidgeClassifier(),
        RidgeClassifierCV(),
        SGDClassifier(),
        OneVsRestClassifier(SVC(kernel='linear')),
        OneVsRestClassifier(LogisticRegression()),
        KNeighborsClassifier()
    ],
    [
        CountVectorizer(),
        TfidfVectorizer(),
        HashingVectorizer()
    ],
    learn,
    test
)

```
---
### 找到精度最高的分类器和矢量器组合

---
![](https://miro.medium.com/max/640/1*jm7ZhN4Z6FlvF8TtKm2W8g.webp)

---
#### TfidfVectorizer()

---
词频 (term frequency, TF) 指的是某一个给定的词语在该文件中出现的次数。
![](https://ai-studio-static-online.cdn.bcebos.com/e04084ae594c4a899c89be0d6f8800486dd8e9f0a6f74a44a75f095d2833c2e8)

---
逆向文件频率 (inverse document frequency, IDF) IDF的主要思想是：如果包含词条t的文档越少, IDF越大，则说明词条具有很好的类别区分能力。某一特定词语的IDF，可以由总文件数目除以包含该词语之文件的数目，再将得到的商取对数得到。
![](https://ai-studio-static-online.cdn.bcebos.com/b6acd527809b4b04aee804d24e5964c8d10c3e8a0c3c482789d96e26dd7f1c7b)

---
某一特定文件内的高词语频率，以及该词语在整个文件集合中的低文件频率，可以产生出高权重的TF-IDF。因此，TF-IDF倾向于过滤掉常见的词语，保留重要的词语。
![](https://ai-studio-static-online.cdn.bcebos.com/c91d0dffb9ca42beafafc82e1bc53a90836b5ed3fbcc456caea3232863dbf170)

---
#### OneVsRestClassifier(SVC(kernel='linear'))

---
