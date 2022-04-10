# unordered_set

```
#include<iostream>
#include<unordered_set>
#include<string>


using namespace std;

int main() {

	unordered_set<string> set;

	//set.emplace("a");
	//set.emplace("a");
	//set.emplace("b");

	set.insert("a");
	set.insert("a");
	set.insert("b");


	for (auto i : set) {
		cout << i << endl;
	}

	cout << "size:" << set.size() << endl;

	return 0;
}

```

没什么好解释的 用 `emplace` 而不用 `insert`