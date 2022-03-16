[TOC]



# CS 97SI

https://web.stanford.edu/class/cs97si/

## [Coding Exercise](https://web.stanford.edu/class/cs97si/assn1.html)

### 1000 A+B Problem

```
#include <iostream>
using namespace std;

int main(){
    int a,b;
    cin>>a>>b;
    cout<<a+b<<endl;
}
```

### 1004 Financial Management

```
#include <iostream>
using namespace std;

float sum;

int main(){
    float m=0;
    for(int i=0;i<12;i++)
    {
        cin>>m;
        sum+=m;
    }
    printf("$%.2f\n",sum/12.0);
    return 0;
}
```



###  1003 Hangover

```
#include <iostream>
using namespace std;

int main()
{
    while (1)
    {
        float n;
        float sum = 0;
        cin>>n;
        if(n == 0.00) break;
        int i=2;
        for(;sum<n;i++){
            sum += 1.0/i;
        }
        cout<<i-2<<" card(s)"<<endl;
    }
    return 0;
}
```

## [Mathematics](https://web.stanford.edu/class/cs97si/assn2.html)

