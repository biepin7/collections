# map

```
#include <unordered_map>

unordered_map<int, int> m;

```



## 提取kv操作

```
std::vector<Key> keys;
keys.reserve(map.size());
std::vector<Val> vals;
vals.reserve(map.size());

for(auto kv : map) {
    keys.push_back(kv.first);
    vals.push_back(kv.second);  
} 

```

## 提取 k 操作

```
//从 m 里取出所有的 key
        vector<int> keys;
        keys.reserve(m.size());
        for (auto &[k, _] : m) {
            keys.push_back(k);
        }
```