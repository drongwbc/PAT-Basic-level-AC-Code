### 0、说一些话

**开始时间：2020. 4. 9**

**完成时间：2020. 4. 27**

<a href="https://pintia.cn/problem-sets/994805260223102976/problems/type/7" target="_blank">PAT乙级题目集</a>

总的来说，乙级题目刚开始做可能会感觉困难，不太好适应这种编程风格，慢慢的就习惯了，做题的思路也来得越来越快，好多题都是思路很简单但代码十分繁琐。学会C++的基础语法，不需要面向对象的部分，在学会STL几种容器的使用方法和它们的操作函数，刷乙级题的知识储备就足够了。(部分题涉及到了排序算法，但题中有解释)

Java做题也可以，也有许多便利的函数(方法)，但Java效率太低，超时是一大问题

### 1001 害死人不偿命的(3n+1)猜想

```c++
#include <iostream>

using namespace std;

int main() {
    int step=0;
    int n;
    cin >> n;
    for(;n!=1;step++){
        if(n%2==0){
            n=n/2;
        }else{
            n=(3*n+1)/2;
        }
    }
    cout << step << endl;
    return 0;
}
```

### 1002 写出这个数
```c++
#include <iostream>
#include <string>
#include <sstream>

using namespace std;

int main() {
    string str;
    cin >> str;
    int sum=0;
    for(int i=1; i<=str.length(); i++) {
        sum=sum+((int)str[i-1]-(int)'0');
    }
    string result;
    stringstream ss;
    ss << sum;
    result=ss.str();
    for(int i=1; i<=result.length(); i++) {
        switch(result[i-1]) {
        case '0':
            cout << "ling";
            break;
        case '1':
            cout << "yi";
            break;
        case '2':
            cout << "er";
            break;
        case '3':
            cout << "san";
            break;
        case '4':
            cout << "si";
            break;
        case '5':
            cout << "wu";
            break;
        case '6':
            cout << "liu";
            break;
        case '7':
            cout << "qi";
            break;
        case '8':
            cout << "ba";
            break;
        case '9':
            cout << "jiu";
            break;
        }
        if(i!=result.length()){
            cout << " ";
        }
    }
}
```

### 1003 我要通过
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>
#include <regex>

//条件三的意思是，aPbP，b一定是A组成的，b中A的个数减一=p中含子串a的个数，如果a不是空

using namespace std;

bool check1(string str) {
    int len = str.size();
    int havep = str.find('P');
    int havea = str.find('A');
    int havet = str.find('T');
    if(havep == -1 || havea == -1 || havet == -1)
        return false;
    for(int i = 1; i <= len; i++) {
        if(str[i - 1] != 'P' && str[i - 1] != 'A' && str[i - 1] != 'T')
            return false;
    }
    return true;
}

bool check2(string str) {
    int len = str.size();
    for(int i = 1; i <= len; i++) {
        if(str[i - 1] != 'A') {
            return false;
        }
    }
    return true;
}

int main() {
    int n;
    cin >> n;
    int result[n] = {0}; //1符合，-1不符合
    for(int i = 1; i <= n; i++) {
        string str;
        cin >> str;
        if(!check1(str)) {
            result[i - 1] = -1;
            continue;
        } else {
            int index = str.find("PAT");
            if(index != -1) {
                if(!check2(str.substr(0, index)) || !check2(str.substr(index + 3, -1))) {
                    result[i - 1] = -1;
                    continue;
                }
            } else {
                if(!regex_match(str, regex("[A]*P{1}[A]+T{1}[A]*"))) {
                    result[i - 1] = -1;
                    continue;
                } else {
                    int index1 = str.find('P');
                    int index2 = str.find('T');
                    int adda = index2 - index1 - 2;
                    int len1 = index1;
                    int len2 = str.size() - index2 - 1;
                    if(len2 <= len1 * adda && len1 != 0) {
                        result[i - 1] = -1;
                        continue;
                    }
                }
            }
        }
        result[i - 1] = 1;
    }
    for(int i = 1; i <= n; i++) {
        if(result[i - 1] == -1) {
            cout << "NO" << endl;
        } else {
            cout << "YES" << endl;
        }
    }
    return 0;
}
```

### 1004 成绩排名
```c++
#include <iostream>

using namespace std;

int main()
{
    int n;
    cin >> n;
    string name[n];
    string id[n];
    int score[n];
    for(int i=1;i<=n;i++){
        cin >> name[i-1] >> id[i-1] >> score[i-1];
    }
    int maxindex=0;
    int minindex=0;
    int max=score[0];
    int min=score[0];
    for(int i=1;i<=n-1;i++){
        if(score[i-1]>max){
            maxindex=i-1;
            max=score[i-1];
        }else if(score[i-1]<min){
            minindex=i-1;
            min=score[i-1];
        }
    }
    cout << name[maxindex] << " " << id[maxindex] << endl;
    cout << name[minindex] << " " << id[minindex] << endl;
    return 0;
}
```

### 1005 继续(3n+1)猜想
```c++
#include <iostream>
#include <algorithm>
#include <set>
#include <vector>

using namespace std;

int main() {
    int k;
    cin >> k;
    int num[k];
    set<int> sum;
    for(int i=1;i<=k;i++){
        cin >> num[i-1];
        int part=num[i-1];
        while(part!=1){
            if(part%2==0){
                part=part/2;
            }else{
                part=(3*part+1)/2;
            }
            sum.insert(part);
        }
    }
    vector<int> ve;
    for(int i=1;i<=k;i++){
        int begin=sum.size();
        sum.insert(num[i-1]);
        int end=sum.size();
        if(end!=begin){
            ve.push_back(num[i-1]);
        }
    }
    sort(ve.begin(),ve.end(),greater<int>{});
    int len=ve.size();
    for(int i=1;i<=len;i++){
        cout << ve.at(i-1);
        if(i!=len){
            cout << " ";
        }
    }
    return 0;
}
```

### 1006 换个格式输出整数
```c++
#include <iostream>
#include <algorithm>

using namespace std;

int main() {
    int n;
    cin >> n;
    string str;
    for(int i=1;i<=n/100;i++){
        str=str+'B';
    }
    for(int i=1;i<=n%100/10;i++){
        str=str+'S';
    }
    for(int i=1;i<=n%10;i++){
        str+=(i+'0');
    }
    cout << str << endl;
    return 0;
}
```

### 1007 ★素数对猜想★
```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <math.h>

//判断素数从1到sqrt(num)即可，否则会超时

using namespace std;

bool ifvegetable(int a){
    for(int i=2;i<=sqrt(a);i++){
        if(a%i==0){
            return false;
        }
    }
    return true;
}

int main() {
    int n;
    cin >> n;
    vector<int> num;
    for(int i=3;i<=n;i++){
        if(ifvegetable(i)){
           num.push_back(i);
        }
    }
    int result=0;
    int len=num.size();
    for(int i=2;i<=len;i++){
        if(num[i-1]-num[i-2]==2){
            result++;
        }
    }
    cout << result << endl;
    return 0;
}
```

### 1008 数组元素循环右移问题
```c++
#include <iostream>
#include <algorithm>

using namespace std;

int main() {
    int n,m;
    cin >> n >> m;
    int step=m%n;
    int num[n];
    for(int i=1; i<=n; i++) {
        cin >> num[i-1];
    }
    for(int i=n-step+1; i<=n; i++) {
        cout << num[i-1] << " ";
    }
    for(int i=1; i<=n-step; i++) {
        cout << num[i-1];
        if(i!=n-step) {
            cout << " ";
        }
    }
    return 0;
}
```

### 1009 说反话
```c++
#include <iostream>
#include <algorithm>
#include <stack>
#include <sstream>

//字符串流在流出时遇空格停止一次

using namespace std;

int main() {
    string str;
    getline(cin,str);
    stringstream ss;
    ss << str;
    stack<string> st;
    while(ss >> str){
        st.push(str);
    }
    while(!st.empty()){
        cout << st.top();
        if(st.size()!=1){
            cout << " ";
        }
        st.pop();
    }
    return 0;
}
```

### 1010 一元多项式求导
```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <stdio.h>

//若结果只有0，应输出0 0，表示系数和指数为0
//输入系数和指数时，输入结束的标志不是输入指数为0，而是按下回车
//总之输出结果应符合人的书写习惯
//尽量不要用size()函数作为循环条件，它易变

using namespace std;

int main() {
    vector<int> ve(0);
    while(true) {
        int num;
        cin >> num;
        ve.push_back(num);
        char ch;
        ch=getchar();
        if(ch=='\n') {
            break;
        }
    }
    int len=ve.size();
    vector<int> re(0);
    for(int i=1; i<=len; i=i+2) {
        int first=ve.at(i-1);
        int second=ve.at(i);
        if(first!=0&&second!=0) {
            re.push_back(second*first);
            re.push_back(second-1);
        } else if(first==0&&second==0) {
            re.push_back(0);
            re.push_back(0);
        }
    }
    if(re.size()!=0) {
        for(auto it=re.begin(); it!=re.end(); it++) {
            if(it!=re.end()-1) {
                cout << *it << " ";
            } else {
                cout << *it << endl;
            }
        }
    }else {
        cout << 0 << " " << 0;
    }
    return 0;
}
```

### 1011 A+B和C
```c++
#include <iostream>

using namespace std;

int main() {
    int n;
    cin >> n;
    long num[n][3];
    for(int i=1;i<=n;i++){
        cin >> num[i-1][0] >> num[i-1][1] >> num[i-1][2];
    }
    for(int i=1;i<=n;i++){
        if(num[i-1][0]+num[i-1][1]>num[i-1][2]){
            cout << "Case " << "#" << i << ": true" << endl;
        }else{
            cout << "Case " << "#" << i << ": false" << endl;
        }
    }
    return 0;
}
```

### 1012 数字分类
```c++
#include <iostream>
#include <stdio.h>

//sum2的结果可能为0，不能以它是否为0判断该类数是否存在

using namespace std;

int main() {
    int n;
    cin >> n;
    int arr[n];
    for(int i=1; i<=n; i++) {
        cin >> arr[i-1];
    }
    int sum1=0;
    int sum2=0;
    int flag2=1;
    bool b2=false;
    int sum3=0;
    int len4=0;
    double sum4=0;
    int sum5=0;
    for(int i=1; i<=n; i++) {
        int num=arr[i-1];
        if(num%5==0&&num%2==0) {
            sum1=sum1+num;
        } else if(num%5==1) {
            sum2=sum2+flag2*num;
            flag2=flag2*(-1);
            b2=true;
        } else if(num%5==2) {
            sum3++;
        } else if(num%5==3) {
            len4++;
            sum4=sum4+num;
        } else if(num%5==4&&num>sum5) {
            sum5=num;
        }
    }
    if(sum1!=0) {
        cout << sum1 << " ";
    } else {
        cout << "N ";
    }
    if(b2) {
        cout << sum2 << " ";
    } else {
        cout << "N ";
    }
    if(sum3!=0) {
        cout << sum3 << " ";
    } else {
        cout << "N ";
    }
    if(sum4!=0) {
        sum4=sum4/len4;
        if((int)sum4!=sum4) {
            printf("%.1lf ",sum4);
        } else {
            cout << sum4 << " ";
        }
    } else {
        cout << "N ";
    }
    if(sum5!=0) {
        cout << sum5;
    } else {
        cout << "N";
    }
    return 0;
}
```

### 1013 数素数
```c++
#include <iostream>
#include <math.h>
#include <vector>

using namespace std;

bool ifvegetable(int m) {
    for(int i=2; i<=sqrt(m); i++) {
        if(m%i==0) {
            return false;
        }
    }
    return true;
}

int main() {
    vector<int> ve(0);
    int m,n;
    cin >> m >> n;
    for(int i=2; ve.size()!=n; i++) {
        if(ifvegetable(i)) {
            ve.push_back(i);
        }
    }
    int flag=1;
    for(int i=m; i<=n; i++,flag++) {
        if(flag%10!=0&&i!=n) {
            cout << ve.at(i-1) << " ";
        } else {
            cout << ve.at(i-1) << endl;
        }
    }
    return 0;
}
```

### 1014 福尔摩斯的约会
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>
#include <math.h>

//注意每个字符应取得得范围，别一股脑'A'到'Z'

using namespace std;

int main() {
    string str1;
    string str2;
    cin >> str1 >> str2;
    int themin = min(str1.size(), str2.size());
    char week = '0';
    char hour = '0';
    for(int i = 1; i <= themin; i++) {
        char ch = str1[i - 1];
        if(ch >= 'A' && ch <= 'G' && ch == str2[i - 1] && week == '0') {
            week = ch;
            continue;
        }
        if(ch == str2[i - 1] && week != '0' && ((ch >= 'A' && ch <= 'N')||(ch>='0'&&ch<='9'))) {
            hour = ch;
            break;
        }
    }
    string str3;
    string str4;
    cin >> str3 >> str4;
    int minute = 0;
    int themin2 = min(str3.size(), str4.size());
    for(int i = 1; i <= themin2; i++) {
        char ch = str3[i - 1];
        if((ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z')) {
            if(ch == str4[i - 1]) {
                minute = i - 1;
                break;
            }
        }

    }
    if(week == 'A') {
        cout << "MON ";
    } else if(week == 'B') {
        cout << "TUE ";
    } else if(week == 'C') {
        cout << "WED ";
    } else if(week == 'D') {
        cout << "THU ";
    } else if(week == 'E') {
        cout << "FRI ";
    } else if(week == 'F') {
        cout << "SAT ";
    } else if(week == 'G') {
        cout << "SUN ";
    }
    if(hour >= '0' && hour <= '9') {
        cout << '0' << hour << ":";
    } else if(hour >= 'A' && hour <= 'N') {
        cout << (hour - 'A') + 10 << ":";
    }
    printf("%02d\n", minute);
    return 0;
}
```

### 1015 ★德才论★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <set>
#include <iterator>

//结构体存储数据
//自定义set容器的排序方式
//注意超时问题，输入尽量scanf，输出尽量printf

using namespace std;

struct student {
    int sum;//总分
    string id;//学号
    int de;//德分
    int cai;//才分
};

struct sortstudent {
    bool operator() (const student& str1, const student& str2) const {
        if(str1.sum != str2.sum)
            return str1.sum > str2.sum;
        else if(str1.sum == str2.sum && str1.de != str2.de)
            return str1.de > str2.de;
        else
            return str1.id < str2.id;
    }
};

int main() {
    int n, l, h;
    cin >> n >> l >> h;
    set<student, sortstudent> result1; //才德兼备
    set<student, sortstudent> result2; //德胜才
    set<student, sortstudent> result3; //“才德兼亡”但尚有“德胜才”
    set<student, sortstudent> result4; //普通合格者
    for(int i = 1; i <= n; i++) {
        char s1[9];
        int s2;
        int s3;
        scanf("%s", s1);
        getchar();
        scanf("%d", &s2);
        getchar();
        scanf("%d", &s3);
        getchar();
        student part;
        part.id = s1;
        part.de = s2;
        part.cai = s3;
        part.sum = part.de + part.cai;
        if(part.de >= h && part.cai >= h) {
            result1.insert(part);
        } else if(part.de >= h && part.cai >= l) {
            result2.insert(part);
        } else if(part.de >= l && part.cai >= l && part.de >= part.cai) {
            result3.insert(part);
        } else if(part.de >= l && part.cai >= l) {
            result4.insert(part);
        }
    }
    cout << result1.size() + result2.size() + result3.size() + result4.size() << endl;
    for(auto it = result1.begin(); it != result1.end(); it++) {
        cout << it->id;
        printf(" %d %d\n", it->de, it->cai);
    }
    for(auto it = result2.begin(); it != result2.end(); it++) {
        cout << it->id;
        printf(" %d %d\n", it->de, it->cai);
    }
    for(auto it = result3.begin(); it != result3.end(); it++) {
        cout << it->id;
        printf(" %d %d\n", it->de, it->cai);
    }
    for(auto it = result4.begin(); it != result4.end(); it++) {
        cout << it->id;
        printf(" %d %d\n", it->de, it->cai);
    }
    return 0;
}
```

### 1016 部分A+B
```c++
#include <iostream>
#include <string>
#include <sstream>

//注意结果为0的情况

using namespace std;

int main() {
    string str1;
    char d1;
    string str2;
    char d2;
    cin >> str1 >> d1 >> str2 >> d2;
    string result1="0";
    int len1=str1.size();
    for(int i=1;i<=len1;i++){
        if(str1[i-1]==d1){
            result1=result1+d1;
        }
    }
    string result2="0";
    int len2=str2.size();
    for(int i=1;i<=len2;i++){
        if(str2[i-1]==d2){
            result2=result2+d2;
        }
    }
    stringstream ss1;
    ss1 << result1;
    int num1;
    ss1 >> num1;
    stringstream ss2;
    ss2 << result2;
    int num2;
    ss2 >> num2;
    cout << num1+num2 << endl;
    return 0;
}
```

### 1017 ★A除以B★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>
#include <sstream>

//注意被除数是一位数的情况
//注意每一步的商大于9的情况，使用to_string

using namespace std;

int main() {
    string str;
    int B;
    cin >> str >> B;
    int len = str.size();
    string Q;
    int begins = 1;
    int nownum = str[begins - 1] - '0';
    if(nownum < 10 && begins == len) {
        cout << nownum / B << " " << nownum % B << endl;
    } else {
        for(int i = begins + 1; i <= len; i++) {
            nownum = nownum * 10 + (str[i - 1] - '0');
            Q += to_string(nownum / B);
            nownum = nownum % B;
        }
        cout << Q << " " << nownum << endl;
    }
    return 0;
}
```

### 1018 锤子剪刀布
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>

//本题倒是没有考虑全输的情况
//注意数组空间与结果的对应

using namespace std;

int main() {
    int n;
    cin >> n;
    int result[3]= {0}; //甲的胜平负
    int winused1[3]= {0}; //甲获胜布石头剪刀
    int winused2[3]= {0}; //乙获胜布石头剪刀
    for(int i=1; i<=n; i++) {
        char ch1;
        char ch2;
        cin >> ch1 >> ch2;
        if(ch1==ch2) {
            result[1]++;
        } else {
            if(ch1=='C') {
                if(ch2=='B') {
                    result[2]++;
                    winused2[0]++;
                } else if(ch2=='J') {
                    result[0]++;
                    winused1[1]++;
                }
            } else if(ch1=='B') {
                if(ch2=='J') {
                    result[2]++;
                    winused2[2]++;
                } else if(ch2=='C') {
                    result[0]++;
                    winused1[0]++;
                }
            } else if(ch1=='J') {
                if(ch2=='C') {
                    result[2]++;
                    winused2[1]++;
                } else if(ch2=='B') {
                    result[0]++;
                    winused1[2]++;
                }
            }
        }
    }
    printf("%d %d %d\n",result[0],result[1],result[2]);
    printf("%d %d %d\n",result[2],result[1],result[0]);
    int index1=1;
    int index2=1;
    int max1=winused1[0];
    int max2=winused2[0];
    for(int i=2; i<=3; i++) {
        if(winused1[i-1]>max1) {
            index1=i;
            max1=winused1[i-1];
        }
        if(winused2[i-1]>max2) {
            index2=i;
            max2=winused2[i-1];
        }
    }
    switch(index1) {
    case 1:
        cout << 'B' << " ";
        break;
    case 2:
        cout << 'C' << " ";
        break;
    case 3:
        cout << 'J' << " ";
        break;
    }
    switch(index2) {
    case 1:
        cout << 'B' << endl;
        break;
    case 2:
        cout << 'C' << endl;
        break;
    case 3:
        cout << 'J' << endl;
        break;
    }
    return 0;
}
```

### 1019 数字黑洞
```c++
#include <iostream>
#include <sstream>
#include <algorithm>
#include <string>
#include <stdio.h>

//输入时不够四位数要补零
//输出时（a + b = c），c要凑齐四位，不够补零，下次循环计算也按四位数算

using namespace std;

int main() {
    string str;
    cin >> str;
    int len=str.size();
    for(int i=1; i<=4-len; i++) {//不够四位数补成四位数
        str='0'+str;
    }
    while(true) {
        stringstream ssa;
        stringstream ssb;
        string stra;
        string strb;

        sort(str.begin(),str.end(),greater<char> {});
        ssa << str;
        stra=str;
        int a;
        ssa >> a;

        sort(str.begin(),str.end());
        strb=str;
        ssb << str;
        int b;
        ssb >> b;

        int c=a-b;
        cout << stra << " - " << strb << " = ";
        printf("%04d\n",c);

        if(c==6174||c==0) {
            break;
        }

        str=to_string(c);

        int len=str.size();
        for(int i=1; i<=4-len; i++) {//结果不够四位数补成四位数
            str='0'+str;
        }
    }
    return 0;
}
```

### 1020 月饼
```c++
#include <iostream>
#include <stdio.h>

//月饼库存可能为小数
//注意库存量小于需求量

using namespace std;

int main() {
    int n,d;
    cin >> n >> d;
    float have[n];
    float sumhave=0;
    for(int i=1; i<=n; i++) {
        scanf("%f",&have[i-1]);
        sumhave=sumhave+have[i-1];
    }
    float price[n];
    for(int i=1; i<=n; i++) {
        float sum;
        scanf("%f",&sum);
        price[i-1]=sum/have[i-1];
    }
    float result=0;
    if(sumhave<=d) {
        for(int i=1; i<=n; i++) {
            result=result+price[i-1]*have[i-1];
        }
    } else {
        int nowhave=0;
        while(nowhave<d) {
            float maxprice=price[0];
            int used=1;
            for(int i=2; i<=n; i++) {
                if(price[i-1]>=maxprice&&have[i-1]!=0) {
                    maxprice=price[i-1];
                    used=i;
                }
            }
            if(nowhave+have[used-1]<=d) {
                result=result+have[used-1]*price[used-1];
            } else {
                result=result+(d-nowhave)*price[used-1];
            }
            nowhave=nowhave+have[used-1];
            have[used-1]=0;
        }
    }
    printf("%.2f",result);
    return 0;
}
```

### 1021 个位数统计
```c++
#include <iostream>
#include <stdio.h>
#include <string>
#include <sstream>

using namespace std;

int main() {
    int num[10]={0};
    string str;
    cin >> str;
    int len=str.size();
    for(int i=1;i<=len;i++){
        stringstream ss;
        int n;
        ss << str[i-1];
        ss >> n;
        num[n]++;
    }
    for(int i=0;i<=9;i++){
        if(num[i]!=0){
            cout << i << ":" << num[i] << endl;
        }
    }
    return 0;
}
```

### 1022 ★D进制的A+B★
```c++
#include <iostream>
#include <algorithm>
#include <stack>

//使用了栈结构，实现了十进制转任意进制
//注意0时要返回0

using namespace std;

string changesystem(int m,int n) {
    stack<char> st;
    string result;
    while(m!=0) {
        int num=m%n;
        char ch;
        if(num<=9) {
            ch=num+'0';
        } else {
            ch=(num-10)+'A';
        }
        st.push(ch);
        m=m/n;
    }
    if(st.empty()){
        return "0";
    }
    while(!st.empty()) {
        result=result+st.top();
        st.pop();
    }
    return result;
}

int main() {
    int a;
    int b;
    int d;
    cin >> a >> b >> d;
    cout << changesystem(a+b,d);
    return 0;
}
```

### 1023 组个最小数
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>

using namespace std;

int main() {
    int num[10] = {0};
    for(int i = 1; i <= 10; i++) {
        cin >> num[i - 1];
    }
    string result;
    for(int i = 1; i <= 10; i++) {
        for(int a = 1; a <= num[i - 1]; a++) {
            result += ((i - 1) + '0');
        }
    }
    if(result[0] == '0') {
        int len = result.size();
        for(int i = 2; i <= len; i++) {
            if(result[i - 1] != '0') {
                result[0] = result[i - 1];
                result[i - 1] = '0';
                break;
            }
        }
    }
    cout << result << endl;
    return 0;
}
```

### 1024 科学计数法
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <math.h>

//没必要把结果放进一个大的字符串，最后在输出，可以一点点输出

using namespace std;

int main() {
    string str;
    cin >> str;
    int index = str.substr(0, str.find('E')).size();
    int num = index;
    while(str[index - 1] == '0') {
        index--;
    }
    num = num - index; //获得有几个后置零
    string str1 = str.substr(1, str.find('E') - 1); //获得前面的数的字符串
    int last = stoi(str.substr(str.find('E') + 1, -1)); //获得后面的数
    if(str[0] == '-')
        cout << "-";
    int len = str1.size();
    if(last < 0) {
        cout << "0.";
        for(int i = 1; i <= fabs(last) - 1; i++)
            cout << '0';

        for(int i = 1; i <= len; i++) {
            if(str1[i - 1] != '.') {
                cout << str1[i - 1];
            }
        }

    } else if(last > 0) {
        int i;
        for(i = 1; i <= len && i <= last + 2; i++) {
            if(str1[i - 1] != '.')
                cout << str1[i - 1];
        }
        if(i <= len) {
            cout << '.';
            for(int a = i; a <= len; a++) {
                cout << str1[a - 1];
            }
        } else {
            for(int a = i - 2; a <= last; a++) {
                cout << '0';
            }
        }
    } else {
        cout << str1 << endl;
    }
    return 0;
}
```

### 1025 ★反转链表★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>

//非原创，自己写的总是超时得22分，下面有
//时间复杂度转换为空间复杂度，巧妙运用数组下标
//静态链表

using namespace std;

int main() {
    int first, n, k;
    cin >> first >> n >> k;
    int test;
    int data[100000];
    int next[100000];
    for(int i = 1; i <= n; i++) {
        scanf("%d", &test);
        scanf("%d%d", &data[test], &next[test]);
    }
    int sum = 0;
    int address[100000];
    while(first != -1) {
        address[sum] = first;
        first = next[first];
        sum++;
    }
    for(int i = 1; i < sum - sum % k; i += k) {
        reverse(address + i - 1, address + i - 1 + k); //反转函数
    }
    for(int i = 1; i <= sum - 1; i++) {
        printf("%05d %d %05d\n", address[i - 1], data[address[i - 1]], address[i]);
    }
    printf("%05d %d %d\n", address[sum - 1], data[address[sum - 1]], -1);
    return 0;
}

--------------------原创的超时代码--------------------

#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <vector>

using namespace std;

struct Node {
    int address;
    int data;
    int next;
};

int main() {
    int first, n, k;
    scanf("%d%d%d", &first, &n, &k);
    vector<int> test1;
    vector<int> test2;
    vector<int> test3;
    for(int i = 1; i <= n; i++) {
        Node part;
        scanf("%d%d%d", &part.address, &part.data, &part.next);
        test1.push_back(part.address);
        test2.push_back(part.data);
        test3.push_back(part.next);
    }
    vector<Node> ve;
    int index = 0;
    for(int i = 1; i <= n; i++) {
        Node part;
        part.address = test1.at(i - 1);
        part.data = test2.at(i - 1);
        part.next = test3.at(i - 1);
        if(part.next != -1 && find(test1.begin(), test1.end(), part.next) == test1.end())
            continue;
        if(part.address != first && find(test3.begin(), test3.end(), part.address) == test3.end())
            continue;
        ve.push_back(part);
        if(part.address == first)
            index = ve.size();
    }
    n = ve.size();
    vector<Node> biao;
    biao.push_back(ve.at(index - 1));
    while(true) {
        int thenext = biao.back().next;
        if(thenext == -1)
            break;
        else {
            for(vector<Node>::iterator it = ve.begin(); it != ve.end(); it++) {
                if((*it).address == thenext) {
                    biao.push_back(*it);
                    ve.erase(it);
                    break;
                }
            }
        }
    }
    vector<Node> result;
    for(int i = 1; i <= n / k; i++) {
        for(int a = 1; a <= k; a++) {
            Node part;
            part.address = biao.at(i * k - a).address;
            part.data = biao.at(i * k - a).data;
            if(a != k)//普通
                part.next = biao.at(i * k - a - 1).address;
            else if(i != n / k)//恰好第k个且有下一个k个
                part.next = biao.at((i + 1) * k - 1).address;
            else if(i * k != n)//恰好第k个，但没有有下一个k个，有不反转的
                part.next = biao.at(i * k).address;
            else//链表反转完毕
                part.next = -1;
            result.push_back(part);
        }
    }
    for(int i = n % k; i >= 1; i--) {
        result.push_back(biao.at(n - i));
    }
    for(int i = 1; i < n; i++) {
        printf("%05d %d %05d\n", result.at(i - 1).address, result.at(i - 1).data, result.at(i - 1).next);
    }
    printf("%05d %d %d\n", result.at(n - 1).address, result.at(n - 1).data, result.at(n - 1).next);
    return 0;
}





```

### 1026 程序运行时间
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <math.h>

using namespace std;

int main() {
    double a1, a2;
    cin >> a1 >> a2;
    int sum = round((a2 - a1) / 100);
    int hour = sum / 3600;
    sum = sum - hour * 3600;
    int minute = sum / 60;
    sum = sum - minute * 60;
    int second = sum;
    printf("%02d:%02d:%02d", hour, minute, second);
    return 0;
}
```

### 1027 打印沙漏
```c++
#include <iostream>

using namespace std;

int main() {
    int n;
    char ch;
    cin >> n >> ch;
    int row=0;
    while(row*(2*row+4)<=(n-1)){
        row++;
    }
    row--;//上下方各有几行
    for(int i=1;i<=row;i++){
        for(int m=1;m<=i-1;m++){
            cout << " ";
        }
        for(int m=1;m<=(2*row+1)-(i-1)*2;m++){
            cout << ch;
        }
        cout << endl;
    }
    for(int i=1;i<=row;i++){
        cout << " ";
    }
    cout << ch <<endl;
    for(int i=1;i<=row;i++){
        for(int m=1;m<=row-i;m++){
            cout << " ";
        }
        for(int m=1;m<=2*i+1;m++){
            cout << ch;
        }
        cout << endl;
    }
    cout << n-1-row*(2*row+4) << endl;
    return 0;
}
```

### 1028 人口普查
```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <sstream>
#include <string>

//输入时使用scanf输入char数组，在赋值给string，否则超时
//该程序也有可能超时，多提交几次
//注意没有合法身份的情况，输出0

using namespace std;

int check(string str) {
    int year;
    int month;
    int day;
    stringstream ss1;
    ss1 << str.substr(0,4);
    ss1 >> year;
    stringstream ss2;
    ss2 << str.substr(5,2);
    ss2 >> month;
    stringstream ss3;
    ss3 << str.substr(8,2);
    ss3 >> day;
    if(year<1814||year>2014) {
        return -1;
    } else if((year==1814&&month<9)||(year==1814&&month==9&&day<6)) {
        return -1;
    } else if((year==2014&&month>9)||(year==2014&&month==9&&day>6)) {
        return -1;
    }
    return (31-day)+(12-month-1)*31+(2014-year-1)*372+285;
}

int main() {
    int n;
    cin >> n;
    vector<string> name;
    vector<int> bir;
    for(int i=1; i<=n; i++) {
        char s1[10];
        char s2[15];
        scanf("%s%s",s1,s2);
        string str1=s1;
        string str2=s2;
        int age=check(str2);
        if(age!=-1) {
            name.push_back(str1);
            bir.push_back(age);
        }
    }
    int len=name.size();
    if(len==0) {
        cout << "0" << endl ;
    } else {
        int old=1;
        int maxage=bir.at(0);
        int youth=1;
        int minage=bir.at(0);
        for(int i=2; i<=len; i++) {
            int age=bir.at(i-1);
            if(age>maxage) {
                maxage=age;
                old=i;
            } else if(minage>age) {
                minage=age;
                youth=i;
            }
        }
        cout << len << " " << name.at(old-1) << " " << name.at(youth-1) << endl;
    }
    return 0;
}
```

### 1029 旧键盘
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <string>
#include <set>

using namespace std;

bool check(char ch, string str) {
    int len = str.size();
    for(int i = 1; i <= len; i++) {
        if(str[i - 1] == ch) {
            return true;
        }
    }
    return false;
}

int main() {
    string str1, str2;
    cin >> str1 >> str2;
    string result;
    int len = str1.size();
    set<char> flag;
    for(int i = 1; i <= len; i++) {
        char ch = str1[i - 1];
        if(!check(ch, str2)) {
            if(ch >= 'a' && ch <= 'z') {
                ch = ch - 32;
            }
            int begins = flag.size();
            flag.insert(ch);
            int ends = flag.size();
            if(ends - begins == 1) {
                result += ch;
            }
        } else {
            continue;
        }
    }
    cout << result << endl;
    return 0;
}
```

### 1030 ★完美数列★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <vector>

//乙级原题，换了个数据结构写了写

using namespace std;

long n;
long p;
vector<long> num;
int result = 1;

int main() {
    cin >> n >> p;
    for(int i = 1; i <= n; i++) {
        long temp;
        cin >> temp;
        num.push_back(temp);
    }
    sort(num.begin(), num.end());
    for(long i = n; i > result; i--) {
        long j;
        for(j = i - result; j >= 1; j--) {
            if(num[i - 1] > num[j - 1]*p) {
                result = i - j;
                break;
            }
        }
        if(j == 0) {
            result = i - j;
            break;
        }
    }
    cout << result << endl;
    return 0;
}
```

### 1031 查验身份证
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>
#include <vector>

using namespace std;

bool check1(string str) {
    for(int i = 1; i <= 17; i++) {
        if(str[i - 1] < '0' || str[i - 1] > '9')
            return false;
    }
    return true;
}

bool check2(string str) {
    char m[11] = {'1', '0', 'X', '9', '8', '7', '6', '5', '4', '3', '2'};
    int sum = 0;
    int part[17] = {7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2};
    for(int i = 1; i <= 17; i++) {
        int thenum = str[i - 1] - '0';
        sum = sum + thenum * part[i - 1];
    }
    int jiaoyan = sum % 11;
    if(str[17] == m[jiaoyan])
        return true;
    else
        return false;
}

int main() {
    int n;
    cin >> n;
    vector<string> ve;
    for(int i = 1; i <= n; i++) {
        string str;
        cin >> str;
        if(!check1(str)) {
            ve.push_back(str);
        } else {
            if(!check2(str)) {
                ve.push_back(str);
            }
        }
    }
    if(ve.size() == 0) {
        cout << "All passed" << endl;
    } else {
        for(auto it : ve) {
            cout << it << endl;
        }
    }
    return 0;
}
```

### 1032 挖掘机技术哪家强
```c++
#include <iostream>
#include <algorithm>
#include <string>

//注意数组索引和学校编号的关系

using namespace std;

int main() {
    int n;
    cin >> n;
    int sum[n]={0};
    for(int i=1;i<=n;i++){
        int school;
        int score;
        cin >> school >> score;
        sum[school-1]=sum[school-1]+score;
    }
    int maxschool=1;
    int maxscore=sum[0];
    for(int i=2;i<=n;i++){
        if(sum[i-1]>maxscore){
            maxscore=sum[i-1];
            maxschool=i;
        }
    }
    cout << maxschool << " " << maxscore << endl;
    return 0;
}
```

### 1033 旧键盘打字
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <string>

//两字符串均有可能为空，getline()什么都能输入

using namespace std;

int main() {
    string str1;
    string str2;
    getline(cin, str1);
    getline(cin, str2);
    int len1 = str1.size();
    bool ifbig = true;
    for(int i = 1; i <= len1; i++) {
        if(str1[i - 1] == '+') {
            ifbig = false;
        }
        if(str1[i - 1] >= 'A' && str1[i - 1] <= 'Z') {
            str1[i - 1] = str1[i - 1] + 32;
        }
    }
    int len2 = str2.size();
    string result;
    for(int i = 1; i <= len2; i++) {
        char part = str2[i - 1];
        bool ifgood = true;
        char ch;
        if(part >= 'A' && part <= 'Z') {
            ch = part + 32;
        } else {
            ch = part;
        }
        for(int a = 1; a <= len1; a++) {
            if(ch == str1[a - 1]) {
                ifgood = false;
                break;
            }
        }
        if(part >= 'A' && part <= 'Z') {
            if(ifbig && ifgood) {
                result += part;
            }
        } else {
            if(ifgood) {
                result += part;
            }
        }
    }
    cout << result << endl;
    return 0;
}
```

### 1034 ★有理数四则运算★
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <math.h>

//辗转相除法求最大公约数，再化简分数，否则超时
//输入的数为整型，但相乘后可能为长整型，用long

using namespace std;

void togetherfirst(long *x, long *y) {
    long a = fabs(*x);
    long b = *y;
    if (a < b) {
        long temp = a;
        a = b;
        b = temp;
    }
    long temp;
    while (b != 0) {
        temp = a % b;
        a = b;
        b = temp;
    }
    *x = *x / a;
    *y = *y / a;
}

string together(long a, long b) {
    if(a == 0)
        return "0";
    if(a % b == 0) {
        if(a > 0)
            return to_string(a / b);
        else
            return '(' + to_string(a / b) + ')';
    } else {
        if(a > b)
            return to_string(a / b) + ' ' + to_string(a % b) + '/' + to_string(b);
        if(-a > b)
            return '(' + to_string(a / b) + ' ' + to_string(-a % b) + '/' + to_string(b) + ')';
        if(a < 0)
            return '(' + to_string(a) + '/' + to_string(b) + ')';
        return to_string(a) + '/' + to_string(b);
    }
}

string add(long a, long b) {
    togetherfirst(&a, &b);
    return together(a, b);
}

string cha(long a, long b) {
    togetherfirst(&a, &b);
    return together(a, b);
}

string cheng(long a, long b) {
    togetherfirst(&a, &b);
    return together(a, b);
}

string chu(long a, long b) {
    if(b < 0) {
        b = -b;
        a = -a;
    }
    togetherfirst(&a, &b);
    return together(a, b);
}


int main() {
    long a1, b1;
    scanf("%ld", &a1);
    getchar();
    scanf("%ld", &b1);
    togetherfirst(&a1, &b1);

    long a2, b2;
    scanf("%ld", &a2);
    getchar();
    scanf("%ld", &b2);
    togetherfirst(&a2, &b2);

    string str1 = together(a1, b1);
    string str2 = together(a2, b2);
    cout << str1 << " + " << str2 << " = " << add(a1 * b2 + a2 * b1, b1 * b2) << endl;
    cout << str1 << " - " << str2 << " = " << cha(a1 * b2 - a2 * b1, b1 * b2) << endl;
    cout << str1 << " * " << str2 << " = " << cheng(a1 * a2, b1 * b2) << endl;
    if(a2 == 0) {
        cout << str1 << " / " << str2 << " = " << "Inf" << endl;
    } else {
        cout << str1 << " / " << str2 << " = " << chu(a1 * b2, a2 * b1) << endl;
    }
    return 0;
}
```

### 1035 ★插入和归并★
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>

//归并排序并非独立解决，归并排序不会

using namespace std;

bool check(int num[], int themiddle[], int n) {//判断中间项是否为插入排序的中间项
    for(int i = 1; i <= n; i++) {
        if(num[i - 1] != themiddle[i - 1]) {
            return false;
        }
    }
    return true;
}

int main() {
    int n;
    cin >> n;
    int num[n];
    int a[n];
    for(int i = 1; i <= n; i++) {
        cin >> num[i - 1];
        a[i-1]=num[i-1];
    }
    int themiddle[n];
    for(int i = 1; i <= n; i++) {
        cin >> themiddle[i - 1];
    }
    bool ifgood = false;
    for(int a = 1; a < n; a++) {
        if(num[a] < num[a - 1]) {
            int temp = num[a];
            int b;
            for(b = a - 1; num[b] > temp; b--) {
                num[b + 1] = num[b];
            }
            num[b + 1] = temp;
        }
        if(ifgood) {
            cout << "Insertion Sort" << endl;
            for(int i = 1; i <= n - 1; i++) {
                cout << num[i - 1] << " ";
            }
            cout << num[n - 1] << endl;
            return 0;
        }
        if(check(num, themiddle, n)) {
            ifgood = true;
        }
    }
    int k = 1, flag = 1;
    while(flag) {
        flag = 0;
        for (int i = 0; i < n; i++) {
            if (a[i] != themiddle[i])
                flag = 1;
        }
        k = k * 2;
        for (int i = 0; i < n / k; i++)
            sort(a + i * k, a + (i + 1) * k);
        sort(a + n / k * k, a + n);
    }
    cout << "Merge Sort" << endl;
    for(int i = 1; i <= n - 1; i++) {
        cout << a[i - 1] << " ";
    }
    cout << a[n - 1] << endl;
    return 0;
}
```

### 1036 跟奥巴马一起编程
```c++
#include <iostream>
#include <math.h>

using namespace std;

int main() {
    int n;
    char ch;
    cin >> n >> ch;
    for(int i=1;i<=n;i++){
        cout << ch;
    }
    cout << endl;
    int row=round(n/2.0);
    for(int i=2;i<=row-1;i++){
        cout << ch;
        for(int a=2;a<=n-1;a++){
            cout << " ";
        }
        cout << ch << endl;
    }
    for(int i=1;i<=n;i++){
        cout << ch;
    }
    return 0;
}
```

### 1037 ★在霍格沃茨找零钱★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <math.h>

//应试编程的巅峰作品

using namespace std;

int main() {
    int price = 0;
    int num;
    cin >> num;
    price += num * 17;
    getchar();//吸收.
    cin >> num;
    price = (price + num) * 29;
    getchar();//吸收.
    cin >> num;
    price += num;
    getchar();//吸收空格

    int sum = 0;
    cin >> num;
    sum += num * 17;
    getchar();//吸收.
    cin >> num;
    sum = (sum + num) * 29;
    getchar();//吸收
    cin >> num;
    sum += num;
    getchar();//吸收空格

    int result = fabs(sum - price);
    int g, s, k;
    s = result / 29;
    k = result - s * 29;
    g = s / 17;
    s = s - g * 17;
    if(sum < price) {
        g = -g;
    }
    printf("%d.%d.%d\n", g, s, k);
    return 0;
}
```

### 1038 统计同成绩学生
```c++
#include <iostream>
#include <stdio.h>

//化时间复杂度为空间复杂度，将0~100所有分数放进数组，否则超时

using namespace std;

int main() {
    long n;
    cin >> n;
    int score[n];
    int sum[101]={0};
    for(int i=1;i<=n;i++){
        scanf("%d",&score[i-1]);
        sum[score[i-1]]++;
    }
    int k;
    cin >> k;
    int goal[k];
    for(int i=1;i<=k;i++){
        scanf("%d",&goal[i-1]);
    }
    for(int i=1;i<=k;i++){
        if(i!=k){
            cout << sum[goal[i-1]] << " ";
        }else{
            cout << sum[goal[i-1]] << endl; ;
        }
    }
    return 0;
}
```

### 1039 到底买不买
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>
#include <iterator>

//字符串中erase的用法同substr相同，需指定被影响字符个数

using namespace std;

int main() {
    string str1;
    string str2;
    cin >> str1 >> str2;
    int len1 = str1.size();
    int len2 = str2.size();
    int sumhave = 0;
    for(int i = 1; i <= len2; i++) {
        int it = str1.find_first_of(str2[i - 1]);
        if(it != -1) {
            str1.erase(it, 1);
            sumhave++;
        }
    }
    if(sumhave == len2) {
        cout << "Yes " << len1 - len2 << endl;
    } else if(sumhave < len2) {
        cout << "No "  << len2 - sumhave << endl;
    }
    return 0;
}
```

### 1040 ★有几个PAT★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>

//注意超时问题
//边遍历边记录需要的数量
//内存溢出，使用long

using namespace std;

int main() {
    string str;
    cin >> str;
    long len = str.size();
    long sum = 0;
    long sumP = 0;
    long sumT = 0;
    long part = 0;
    bool ift = false;//是否开始记录T
    for(long i = 1; i <= len - 1; i++) {
        if(str[i - 1] == 'P') {
            sumP++;
        }
        if(str[i - 1] == 'A') {
            if(!ift) {//计算第一个A后面所有的T
                for(long t = i; t <= len; t++) {
                    if(str[t - 1] == 'T') {
                        sumT++;
                    }
                }
                ift = true;
            }
            sum += sumP * (sumT - part);
        }
        if(str[i - 1] == 'T' && ift) {
            part++;
        }
    }
    cout << sum % 1000000007 << endl;
    return 0;
}
```

### 1041 考试座位号
```c++
#include <iostream>
#include <string>

using namespace std;

int main() {
    int n;
    cin >> n;
    string id[n];
    int seat[n];
    for(int i = 1; i <= n; i++) {
        string name;
        int seat1;//试机号
        int seat2;//考试座位号
        cin >> name >> seat1 >> seat2;
        id[seat1 - 1] = name;
        seat[seat1 - 1] = seat2;
    }
    int m;
    cin >> m;
    int tofind[m];
    for(int i = 1; i <= m; i++) {
        cin >> tofind[i - 1];
    }
    for(int i = 1; i <= m; i++) {
        int seat1 = tofind[i - 1];
        cout << id[seat1 - 1] << " " << seat[seat1 - 1] << endl;
    }
    return 0;
}
```

### 1042 字符统计
```c++
#include <iostream>
#include <algorithm>
#include <string>

//合理运用ASCII码进行字符运算

using namespace std;

int main() {
    string str;
    getline(cin,str);
    int num[26]= {0};
    int len=str.size();
    for(int i=1; i<=len; i++) {
        char ch=str[i-1];
        if(ch>='A'&&ch<='Z') {
            num[ch-'A']++;
        } else if(ch>='a'&&ch<='z') {
            num[ch-'a']++;
        }
    }
    int max=num[0];
    char big='a';
    for(int i=2;i<=26;i++){
        if(num[i-1]>max){
            max=num[i-1];
            big=(char)((int)'a'+i-1);
        }
    }
    cout << big << " " << max << endl;
    return 0;
}
```

### 1043 输出PATest
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>

//合理利用数组，它不仅仅是数的集合，也是事物的代表

using namespace std;

int main() {
    string str;
    cin >> str;
    int len = str.size();
    int letter[6] = {0}; //P,A,T,e,s,t
    for(int i = 1; i <= len; i++) {
        char ch = str[i - 1];
        if(ch == 'P') {
            letter[0]++;
        } else if(ch == 'A') {
            letter[1]++;
        } else if(ch == 'T') {
            letter[2]++;
        } else if(ch == 'e') {
            letter[3]++;
        } else if(ch == 's') {
            letter[4]++;
        } else if(ch == 't') {
            letter[5]++;
        }
    }
    while(letter[0] + letter[1] + letter[2] + letter[3] + letter[4] + letter[5] != 0) {
        if(letter[0] >= 1) {
            cout << 'P';
            letter[0]--;
        }
        if(letter[1] >= 1) {
            cout << 'A';
            letter[1]--;
        }
        if(letter[2] >= 1) {
            cout << 'T';
            letter[2]--;
        }
        if(letter[3] >= 1) {
            cout << 'e';
            letter[3]--;
        }
        if(letter[4] >= 1) {
            cout << 's';
            letter[4]--;
        }
        if(letter[5] >= 1) {
            cout << 't';
            letter[5]--;
        }
    }
    return 0;
}
```

### 1044 火星数字
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>
#include <sstream>
#include <stack>
#include <vector>

//注意火星数字整位的换算
//PAT不能使用gets()函数输入字符串

using namespace std;

string marnum[13] = {"tret", "jan", "feb", "mar", "apr", "may", "jun", "jly", "aug", "sep", "oct", "nov", "dec"};
string marshi[13] = {"", "tam", "hel", "maa", "huh", "tou", "kes", "hei", "elo", "syy", "lok", "mer", "jou"};

string tomar(string str) {
    stringstream ss;
    ss << str;
    int num;
    ss >> num;
    stack<int> st;
    while(num != 0) {
        st.push(num % 13);
        num = num / 13;
    }
    string result;
    if(st.size() == 0) {
        result = marnum[0];
    } else if(st.size() == 1) {
        result += marnum[st.top()];
    } else if(st.size() == 2) {
        result += marshi[st.top()];
        st.pop();
        if(st.top() != 0)
            result += " " + marnum[st.top()];
    }
    return result;
}

string toearth(string str) {
    if(find(marshi, marshi + 13, str) != marshi + 13) {
        return to_string((find(marshi, marshi + 13, str) - marshi) * 13);
    }
    int thespace = str.find(" ");
    if(thespace == -1) {
        return to_string(find(marnum, marnum + 13, str) - marnum);
    } else {
        string str1 = str.substr(0, thespace);
        int num1 = find(marshi, marshi + 13, str1) - marshi;
        string str2 = str.substr(thespace + 1, -1);
        int num2 = find(marnum, marnum + 13, str2) - marnum;
        return to_string(num1 * 13 + num2);
    }
}

int main() {
    int n;
    cin >> n;
    getchar();
    vector<string> result;
    for(int i = 1; i <= n; i++) {
        string str;
        getline(cin, str);
        if(isdigit(str[0])) {
            result.push_back(tomar(str));
        } else {
            result.push_back(toearth(str));
        }
    }
    for(auto it = result.begin(); it != result.end(); it++) {
        cout << *it << endl;
    }
    return 0;
}
```

### 1045 ★快速排序★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <vector>

//排序前后，位置变的一定是主元，但主元不一定位置改变
//比如1 5 2 4 3，4在排序前后位置不变，但它不是主元

using namespace std;

int main() {
    long n;
    cin >> n;
    vector<long> ve1;
    for(long i = 1; i <= n; i++) {
        long num;
        scanf("%ld", &num);
        ve1.push_back(num);
    }
    vector<long> ve2 = ve1;
    sort(ve1.begin(), ve1.end());
    vector<long> result;
    long themax = 0;
    for(long i = 1; i <= n; i++) {
        if(ve2.at(i - 1) == ve1.at(i - 1) && ve2.at(i - 1) > themax) {
            result.push_back(ve2.at(i - 1));
        }
        if(ve2.at(i - 1) > themax) {
            themax = ve2.at(i - 1);
        }
    }
    long len = result.size();
    printf("%ld\n", len);
    for(vector<long>::iterator it = result.begin(); it != result.end(); it++) {
        printf("%ld", *it);
        if(it != (--result.end())) {
            printf(" ");
        }
    }
    printf("\n");
    return 0;
}
```

### 1046 划拳
```c++
#include <iostream>

using namespace std;

int main() {
    int n;
    cin >> n;
    int sum1 = 0; //甲输
    int sum2 = 0; //乙输
    for(int i = 1; i <= n; i++) {
        int a1, a2, b1, b2;
        cin >> a1 >> a2 >> b1 >> b2;
        if(b2 == a1 + b1 && a2 != a1 + b1) {
            sum1++;
        } else if(a2 == a1 + b1 && b2 != a1 + b1) {
            sum2++;
        }
    }
    cout << sum1 << " " << sum2;
    return 0;
}
```

### 1047 编程团体赛
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <map>
#include <sstream>

//利用map容器进行排序操作，同时一对一容纳

using namespace std;

int main() {
    int n;
    cin >> n;
    map<int, int> score;
    for(int i = 1; i <= n; i++) {
        string team;
        cin >> team;
        stringstream ss;
        ss << team;
        int id;
        ss >> id;
        int point;
        cin >> point;
        score[id] = score[id] + point;
    }
    int champion = 0;
    int maxscore = 0;
    for(auto it = score.begin(); it != score.end(); it++) {
        if((it->second) > maxscore) {
            maxscore = it->second;
            champion = it->first;
        }
    }
    cout << champion << " " << maxscore << endl;
    return 0;
}
```

### 1048 数字加密
```c++
#include <iostream>
#include <algorithm>
#include <math.h>
#include <string>
#include <stack>
#include <sstream>

//两字符串长度不同时，需要在短的前面补0，使长度一样在运算

using namespace std;

int main() {
    string stra;
    string strb;
    cin >> stra >> strb;
    int lena=stra.size();
    int lenb=strb.size();
    if(lena<lenb) {
        stringstream ss;
        string temp;
        ss << stra;
        ss >> temp;
        stra="";
        for(int i=1; i<=lenb-lena; i++) {
            stra+=(0+'0');
        }
        stra=stra+temp;
    } else if(lena>lenb) {
        stringstream ss;
        string temp;
        ss << strb;
        ss >> temp;
        strb="";
        for(int i=1; i<=lena-lenb; i++) {
            strb+=(0+'0');
        }
        strb=strb+temp;
    }
    int len=stra.size();
    stack<char> st;
    for(int i=len; i>=1; i--) {
        char ch;
        int num;
        if((len-i+1)%2==0) {
            num=strb[i-1]-stra[i-1];
            if(num<0) {
                num=num+10;
            }
        } else {
            num=((stra[i-1]-'0')+(strb[i-1]-'0'))%13;
        }
        if(num<10) {
            stringstream ss;
            ss << num;
            ss >> ch;
        } else {
            switch(num) {
            case 10:
                ch='J';
                break;
            case 11:
                ch='Q';
                break;
            case 12:
                ch='K';
                break;
            }
        }
        st.push(ch);
    }
    string result;
    while(!st.empty()) {
        result=result+st.top();
        st.pop();
    }
    cout << result << endl;
    return 0;
}
```

### 1049 数列的片段和
```c++
#include <iostream>
#include <algorithm>
#include <string>
#include <stdio.h>

//第i个数出现的次数为：i*(n-i+1)

using namespace std;

int main() {
    int n;
    scanf("%d",&n);
    double num[n];
    double sum=0;
    for(int i=1;i<=n;i++){
        scanf("%lf",&num[i-1]);
        sum=sum+num[i-1]*i*(n-i+1);
    }
    printf("%.2lf\n",sum);
    return 0;
}
```

### 1050 ★螺旋矩阵★
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <math.h>

//行和列的计算很讲究，同时要保证结果行大于列
//循环的次数无法具体确定，所以循环条件为待用数组还未使用完全
//二维数组行列数大于10000会出现溢出
//每一次循环完成一次回圈的填充，右->下->左->上

using namespace std;

int main() {
    int N;
    cin >> N;
    int m = sqrt(N) - 1, n = 1;
    while(m * n != N) {
        m++;
        n = N / m;
    }
    if(m < n) {
        int temp = m;
        m = n;
        n = temp;
    }
    int num[N];
    for(int i = 1; i <= N; i++) {
        cin >> num[i - 1];
    }
    sort(num, num + N, greater<int> {});
    int re[m][n];
    int index = 0;
    for(int flag = 1; index < N; flag++) {
        for(int i = flag; i <= n - flag + 1 && index < N; i++) { //上
            re[flag - 1][i - 1] = num[index++];
        }
        for(int i = flag + 1; i <= m - flag + 1 && index < N; i++) { //右
            re[i - 1][n - flag] = num[index++];
        }
        for(int i = n - flag; i >= flag && index < N; i--) { //下
            re[m - flag][i - 1] = num[index++];
        }
        for(int i = m - flag; i >= flag + 1 && index < N; i--) {//左
            re[i - 1][flag - 1] = num[index++];
        }
    }
    for(int a = 1; a <= m; a++) {
        for(int b = 1; b <= n; b++) {
            cout << re[a - 1][b - 1];
            if(b != n) {
                cout << " ";
            }
        }
        cout << endl;
    }
    return 0;
}
```

### 1051 ★复数乘法★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <math.h>

//注意计算精度，尽量使用double而不是float
//-0.005~0之间的小数保留两位是0.00，不是-0.00

using namespace std;

int main() {
    float r1,p1;
    cin >> r1 >> p1;
    float r2,p2;
    cin >> r2 >> p2;
    float a=r1*cos(p1),b=r1*sin(p1);
    float c=r2*cos(p2),d=r2*sin(p2);
    float m=a*c-b*d;
    float n=a*d+b*c;
    if(m<0&&m>-0.005) {
        m=0;
    }
    printf("%.2f",m);
    if(n<0&&n>-0.005) {
        n=0;
    }
    if(n>=0) {
        printf("+%.2fi",n);
    } else {
        printf("-%.2fi",-n);
    }
    return 0;
}
```

### 1052 ★卖个萌★
```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <string>
#include <stdio.h>

//注意'\'字符需要转义，使用'\\'
//合理利用goto，程序短小更清晰

using namespace std;

vector<string> getemojie(string str) {
    int len = str.size();
    vector<string> ve;
    for(int i = 1; i <= len; i++) {
        if(str[i - 1] == '[') {
            for(int a = i + 2; a <= len; a++) {
                if(str[a - 1] == ']') {
                    ve.push_back(str.substr(i, a - i - 1));
                    i = a;
                    break;
                }
            }
        }
    }
    return ve;
}

int main() {
    string hand;
    string eye;
    string mouth;
    getline(cin, hand);
    getline(cin, eye);
    getline(cin, mouth);
    vector<string> vehand = getemojie(hand);
    vector<string> veeye = getemojie(eye);
    vector<string> vemouth = getemojie(mouth);
    int len1 = vehand.size();
    int len2 = veeye.size();
    int len3 = vemouth.size();
    int k;
    cin >> k;
    vector<string> ve;
    for(int i = 1; i <= k; i++) {
        string result;

        int a;
        cin >> a;
        if(a <= len1 && a >= 1) {
            result += vehand.at(a - 1);
        } else {
            result = "HelloWorld";
            goto meiyou;
        }

        int b;
        cin >> b;
        if(b <= len2 && b >= 1) {
            result += '(' + veeye.at(b - 1);
        } else {
            result = "HelloWorld";
            goto meiyou;
        }

        int c;
        cin >> c;
        if(c <= len3 && c >= 1) {
            result += vemouth.at(c - 1);
        } else {
            result = "HelloWorld";
            goto meiyou;
        }

        int d;
        cin >> d;
        if(d <= len2 && d >= 1) {
            result += veeye.at(d - 1);
        } else {
            result = "HelloWorld";
            goto meiyou;
        }

        int e;
        cin >> e;
        if(e <= len1 && e >= 1) {
            result += ')' + vehand.at(e - 1);
        } else {
            result = "HelloWorld";
            goto meiyou;
        }
meiyou:
        ve.push_back(result);
    }
    for(auto it : ve) {
        if(it == "HelloWorld") {
            it = "Are you kidding me? @\\/@";
        }
        cout << it << endl;
    }
    return 0;
}
```

### 1053 住房空置率
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>

//注意输出百分号需要转义

using namespace std;

int main() {
    int n;
    double e, d;
    cin >> n >> e >> d;
    double re1 = 0; //可能空置
    double re2 = 0; //完全空置
    for(int i = 1; i <= n; i++) {
        int day;
        cin >> day;
        int sum = 0;
        for(int a = 1; a <= day; a++) {
            double num;
            cin >> num;
            if(num < e) {
                sum++;
            }
        }
        if(sum > day / 2 && day <= d) {
            re1++;
        } else if(sum > day / 2 && day > d) {
            re2++;
        }
    }
    printf("%.1f%% %.1f%%\n", 100 * re1 / n, 100 * re2 / n);
    return 0;
}
```

### 1054 ★求平均值★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>
#include <vector>
#include <sstream>

//尽量不使用正则表达式，stl支持较差
//注意最后输出的换行只能有一个，所有题都一样
//一个数时输出number而不是numbers

using namespace std;

bool check(string str) {
    if(count(str.begin(), str.end(), '.') > 1)
        return false;
    int len = str.size();
    int thepoint = str.find('.');
    if(str[0] != '-' && !isdigit(str[0])) {
        return false;
    }
    if(thepoint != -1) {
        if((str.substr(thepoint, -1)).size() > 3) {
            return false;
        }
    }
    for(int i = 2; i <= len; i++) {
        if(!isdigit(str[i - 1]) && (i - 1) != thepoint) {
            return false;
        }
    }
    return true;
}

int main() {
    int n;
    cin >> n;
    vector<double> goods;
    vector<string> bads;
    for(int i = 1; i <= n; i++) {
        string str;
        cin >> str;
        if(check(str)) {
            double num;
            stringstream ss;
            ss << str;
            ss >> num;
            if(num >= -1000 && num <= 1000)
                goods.push_back(num);
            else
                bads.push_back(str);
        } else {
            bads.push_back(str);
        }
    }
    for(auto it = bads.begin(); it != bads.end(); it++) {
        cout << "ERROR: " << *it << " is not a legal number" << endl;
    }
    int len = goods.size();
    double result = 0;
    for(auto it = goods.begin(); it != goods.end(); it++) {
        result = result + (*it) / len;
    }
    if(len == 0) {
        cout << "The average of 0 numbers is Undefined" << endl;
    } else if(len == 1) {
        printf("The average of %d number is %.2lf\n", 1, result);
    } else {
        printf("The average of %d numbers is %.2lf\n", len, result);
    }
    return 0;
}
```

### 1055 ★集体照★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <vector>

//每一排根据人数的奇偶进行排列，先左后右
//将每一排的人（单独）升序排列，在索引输出
//自定义排序器

using namespace std;

struct person {
    string name;
    int height;
};

int cmp(struct person a, struct person b) {
    if(a.height != b.height)
        return a.height > b.height;
    else
        return a.name < b.name;
}

int cmp2(struct person a, struct person b) {
    if(a.height != b.height)
        return a.height < b.height;
    else
        return a.name > b.name;
}

int main() {
    int n, k;
    cin >> n >> k;
    vector<person> ve;
    for(int i = 1; i <= n; i++) {
        person part;
        cin >> part.name >> part.height;
        ve.push_back(part);
    }
    sort(ve.begin(), ve.end(), cmp);
    int persons = n / k;
    int sum;
    if(persons * k != n) {
        sum = n - persons * k + persons;
    } else {
        sum = persons;
    }
    sort(ve.begin(), ve.begin() + sum, cmp2);
    if(sum % 2 == 0) {
        for(int left = 1; left <= sum - 1; left = left + 2) {
            cout << ve.at(left - 1).name << " ";
        }
        for(int right = sum; right >= 2; right = right - 2) {
            cout << ve.at(right - 1).name;
            if(right != 2) {
                cout << " ";
            }
        }
    } else {
        for(int left = 2; left <= sum - 1; left = left + 2) {
            cout << ve.at(left - 1).name << " ";
        }
        for(int right = sum; right >= 1; right = right - 2) {
            cout << ve.at(right - 1).name;
            if(right != 1) {
                cout << " ";
            }
        }
    }
    cout << endl;
    int havechu = sum;
    for(int i = 2; i <= k; i++) {
        sort(ve.begin() + havechu, ve.begin() + havechu + persons, cmp2);
        if(persons % 2 == 0) {
            for(int left = 1; left <= persons - 1; left = left + 2) {
                cout << ve.at(havechu + left - 1).name << " ";
            }
            for(int right = persons; right >= 2; right = right - 2) {
                cout << ve.at(havechu + right - 1).name;
                if(right != 2) {
                    cout << " ";
                }
            }
        } else {
            for(int left = 2; left <= persons - 1; left = left + 2) {
                cout << ve.at(havechu + left - 1).name << " ";
            }
            for(int right = persons; right >= 1; right = right - 2) {
                cout << ve.at(havechu + right - 1).name;
                if(right != 1) {
                    cout << " ";
                }
            }
        }
        cout << endl;
        havechu += persons;
    }
    return 0;
}
```

### 1056 组合数的和
```c++
#include <iostream>

using namespace std;

int main() {
    int n;
    cin >> n;
    int num[n];
    for(int i=1;i<=n;i++){
        cin >> num[i-1];
    }
    int sum=0;
    for(int a=1;a<=n-1;a++){
        for(int b=a+1;b<=n;b++){
            sum=sum+(num[a-1]*10+num[b-1])+(num[b-1]*10+num[a-1]);
        }
    }
    cout << sum << endl;
    return 0;
}
```

### 1057 数壹零
```c++
#include <iostream>
#include <algorithm>
#include <string>

using namespace std;

int main() {
    string str;
    getline(cin,str);
    int len=str.size();
    int num=0;
    for(int i=1;i<=len;i++){
        char ch=str[i-1];
        if(ch>='a'&&ch<='z'){
            num=num+(ch-'a'+1);
        }else if(ch>='A'&&ch<='Z'){
            num=num+(ch-'A'+1);
        }
    }
    int sum0=0;
    int sum1=0;
    while(num!=0){
        int part=num%2;
        if(part==0){
            sum0++;
        }else if(part==1){
            sum1++;
        }
        num=num/2;
    }
    cout << sum0 << " " << sum1 << endl;
    return 0;
}
```

### 1058 选择题
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>
#include <map>
#include <set>

//最初使用map容器，陷入了以为比较value值得想法
//又一个应试编程

using namespace std;

struct problem {
    int score;
    string right;
};

int main() {
    int n, m;
    cin >> n >> m;
    problem order[m];
    for(int i = 1; i <= m; i++) {
        cin >> order[i - 1].score;
        int num;
        cin >> num;
        cin >> num;
        string theright = '(' + to_string(num);
        string rights;
        getline(cin, rights);
        theright += rights + ')';
        order[i - 1].right = theright;
    }
    int score[n] = {0};
    int wrong[m] = {0};
    for(int i = 1; i <= n; i++) {
        for(int a = 1; a <= m; a++) {
            string answer;
            while(true) {
                char ch;
                ch = getchar();
                answer += ch;
                if(ch == ')') {
                    break;
                }
            }
            getchar();//吸收空格或回车
            if(answer == order[a - 1].right) {
                score[i - 1] += order[a - 1].score;
            } else {
                wrong[a - 1]++;
            }
        }
    }
    for(int i = 1; i <= n; i++) {
        cout << score[i - 1] << endl;
    }
    int themax = *max_element(wrong, wrong + m);
    if(themax == 0) {
        cout << "Too simple";
    } else {
        cout << themax;
        for(int i = 1; i <= m; i++) {
            if(wrong[i - 1] == themax) {
                cout << " " << i;
            }
        }
    }
    cout << endl;
    return 0;
}
```

### 1059 ★C语言竞赛★
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <map>
#include <math.h>

//map容器可以用索引访问
//迭代访问容器效率低，容易超时

using namespace std;

bool ifvegetable(int m) {
    for(int i = 2; i <= sqrt(m); i++) {
        if(m % i == 0)
            return false;
    }
    return true;
}

int main() {
    int n;
    cin >> n;
    map<string, int> name;
    for(int i = 1; i <= n; i++) {
        string str;
        cin >> str;
        name[str] = i;
    }
    int k;
    cin >> k;
    int result[k];//-1不存在,0,1,2,3
    string getprize[k];
    for(int i = 1; i <= k; i++) {
        cin >> getprize[i - 1];
        string thename = getprize[i - 1];
        if(name[thename] == 1) {
            result[i - 1] = 0;
        } else if(ifvegetable(name[thename]) && name[thename] > 1 && name[thename] <= n) {
            result[i - 1] = 1;
        } else if(name[thename] > 1 && name[thename] <= n) {
            result[i - 1] = 2;
        } else {
            result[i - 1] = -1;
        }
    }
    for(int i = 1; i <= k; i++) {
        int theresult = result[i - 1];
        string thename = getprize[i - 1];
        cout << thename << ": ";
        if(theresult != -1 && name[thename] == -2) {
            theresult = 3;
        }
        if(theresult == -1) {
            cout << "Are you kidding?" << endl;
        } else if(theresult == 0) {
            cout << "Mystery Award" << endl;
        } else if(theresult == 1) {
            cout << "Minion" << endl;
        } else if(theresult == 2) {
            cout << "Chocolate" << endl;
        } else if(theresult == 3) {
            cout << "Checked" << endl;
        }
        if(theresult != -1) {
            name[thename] = -2;
        }
    }
    return 0;
}
```

### 1060 爱丁顿数
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>

using namespace std;

int main() {
    int n;
    cin >> n;
    int num[n];
    for(int i = 1; i <= n; i++) {
        scanf("%d", &num[i - 1]);
    }
    sort(num, num + n);
    for(int i = n; i >= 0; i--) {
        if(num[n - i] > i) {
            cout << i << endl;
            break;
        }
    }
    return 0;
}
```

### 1061 判断题
```c++
#include <iostream>
#include <algorithm>

//边输入边计算，提高效率

using namespace std;

int main() {
    int n,m;//n学生人数，m题目数量
    cin >> n >> m;
    int point[m];
    for(int i=1;i<=m;i++){
        cin >> point[i-1];
    }
    int right[m];
    for(int i=1;i<=m;i++){
        cin >> right[i-1];
    }
    int answer[n][m];
    int score[n]={0};
    for(int a=1;a<=n;a++){
        for(int b=1;b<=m;b++){
            cin >> answer[a-1][b-1];
            if(answer[a-1][b-1]==right[b-1]){
                score[a-1]=score[a-1]+point[b-1];
            }
        }
    }
    for(int i=1;i<=n;i++){
        cout << score[i-1] << endl;
    }
    return 0;
}
```

### 1062 最简分数
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <math.h>
#include <vector>

//注意通分后分子范围的上下界
//最简分数的分子和分母除了1，没有其他公因数
//第二个分数可能比第一个小，所以到时候需要交换

using namespace std;

bool ifvegetable(int m, int n) {
    int themin = min(m, n);
    for(int i = 2; i <= themin; i++) {
        if(m % i == 0 && n % i == 0)
            return false;
    }
    return true;
}

int main() {
    float n1, m1;
    cin >> n1;
    getchar();
    cin >> m1;
    float n2, m2;
    cin >> n2;
    getchar();
    cin >> m2;
    int k;
    cin >> k;
    int a = (int)((n1 * k) / m1 + 1);
    int b = ceil((n2 * k) / m2 - 1);
    if(a < b) {
        int temp = b;
        b = a;
        a = temp;
    }
    vector<int> ve;
    for(int i = a; i <= b; i++) {
        if(ifvegetable(i, k)) {
            ve.push_back(i);
        }
    }
    int len = ve.size();
    for(int i = 1; i <= len; i++) {
        cout << ve.at(i - 1) << "/" << k;
        if(i != len) {
            cout << " ";
        }
    }
    return 0;
}
```

### 1063 计算谱半径
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <set>
#include <math.h>

using namespace std;

int main() {
    int n;
    cin >> n;
    set<double> num;
    for(int i = 1; i <= n; i++) {
        double a, b;
        cin >> a >> b;
        num.insert(sqrt(a * a + b * b));
    }
    printf("%.2lf", *(--num.end()));
    return 0;
}
```

### 1064 朋友数
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <string>
#include <set>

using namespace std;

int getid(string str) {
    int len = str.size();
    int result = 0;
    for(int i = 1; i <= len; i++) {
        result += str[i - 1] - '0';
    }
    return result;
}

int main() {
    int n;
    cin >> n;
    set<int> id;
    for(int i = 1; i <= n; i++) {
        string str;
        cin >> str;
        id.insert(getid(str));
    }
    int len = id.size();
    cout << len << endl;
    for(auto it = id.begin(); it != id.end(); it++) {
        cout << *it;
        if(it != --id.end()) {
            cout << " ";
        }
    }
    return 0;
}
```

### 1065 ★单身狗★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <map>
#include <set>

//遍历夫妻map容器，在宾客中寻找，找到夫妻一起删除
//如果正常思路遍历宾客容器，会超时
//尽量遍历容量小的容器

using namespace std;

int main() {
    int n;
    scanf("%d", &n);
    map<string, string> partner;
    for(int i = 1; i <= n; i++) {
        char str1[6], str2[6];
        scanf("%s", str1);
        getchar();
        scanf("%s", str2);
        getchar();
        partner[str1] = str2;
    }
    int m;
    scanf("%d", &m);
    set<string> guest;
    for(int i = 1; i <= m; i++) {
        char str[6];
        scanf("%s", str);
        getchar();
        guest.insert(str);
    }
    for(auto it = partner.begin(); it != partner.end(); it++) {
        if(guest.find(it->first) != guest.end() && guest.find(it->second) != guest.end()) {
            guest.erase(it->first);
            guest.erase(it->second);
        }
    }
    cout << guest.size() << endl;
    for(auto it = guest.begin(); it != guest.end(); it++) {
        cout << *it;
        if(it != (--guest.end())) {
            cout << " ";
        }
    }
    return 0;
}
```

### 1066 图像过滤
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>

using namespace std;

int main() {
    int m, n, a, b, change;
    cin >> m >> n >> a >> b >> change;
    int num[m][n];
    for(int row = 1; row <= m; row++) {
        for(int column = 1; column <= n; column++) {
            cin >> num[row - 1][column - 1];
            if(num[row - 1][column - 1] >= a && num[row - 1][column - 1] <= b) {
                num[row - 1][column - 1] = change;
            }
        }
    }
    for(int row = 1; row <= m; row++) {
        for(int column = 1; column <= n; column++) {
            printf("%03d", num[row - 1][column - 1]);
            if(column != n) {
                printf(" ");
            }
        }
        cout << endl;
    }
    return 0;
}
```

### 1067 试密码
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <string>

//输入的密码可能有空格，需要getline()
//getline()，若前面也有输入，需要前面使用getchar()吸收回车

using namespace std;

int main() {
    string password;
    int n;
    cin >> password >> n;
    string str[n];//每一次的输入
    int result[n] = {0}; //-1错误，1正确
    int i = 1;
    getchar();
    while(true) {
        string input;
        getline(cin, input);
        if(input == "#") {
            break;
        }
        if(i <= n) {
            str[i - 1] = input;
            if(str[i - 1] == password) {
                result[i - 1] = 1;
            } else {
                result[i - 1] = -1;
            }
            i++;
        }
    }
    for(int a = 1; a <= n; a++) {
        int theresult = result[a - 1];
        if(theresult == 1) {
            cout << "Welcome in" << endl;
            break;
        } else if(theresult == -1) {
            cout << "Wrong password: " << str[a - 1] << endl;
            if(a == n) {
                cout << "Account locked" << endl;
            }
        }
    }
    return 0;
}
```

### 1068 万绿丛中一点红
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <math.h>

//勉强通过，我承认我有堵的成分，但赌对了

using namespace std;

bool check(int color, int other, int big) {
    if(fabs(color - other)> big)
        return false;
    else
        return true;
}

int main() {
    int m, n, big;
    cin >> m >> n >> big;
    int num[n][m];
    for(int row = 1; row <= n; row++) {
        for(int column = 1; column <= m; column++) {
            cin >> num[row - 1][column - 1];
        }
    }
    int sum = 0;
    int therow = 0;
    int thecolumn = 0;
    for(int row = 1; row <= n; row++) {
        if(sum > 1) {
            break;
        }
        for(int column = 1; column <= m; column++) {
            int color = num[row - 1][column - 1];
            int sumpart = 0;
            if(row - 1 > 0) {//可上移
                if(!check(color, num[row - 2][column - 1], big)) {//上
                    sumpart++;
                }
                if(column - 1 > 0) {//左上
                    if(!check(color, num[row - 2][column - 2], big)) {
                        sumpart++;
                    }
                }
                if(column + 1 <= m) {//右上
                    if(!check(color, num[row - 2][column], big)) {
                        sumpart++;
                    }
                }
            }
            if(column - 1 > 0) { //左
                if(!check(color, num[row - 1][column - 2], big)) {
                    sumpart++;
                }
            }
            if(column + 1 <= m) { //右
                if(!check(color, num[row - 1][column], big)) {
                    sumpart++;
                }
            }
            if(row + 1 <= n) { //可下移
                if(!check(color, num[row][column - 1], big)) { //下
                    sumpart++;
                }
                if(column - 1 > 0) { //左下
                    if(!check(color, num[row][column - 2], big)) {
                        sumpart++;
                    }
                }
                if(column + 1 <= m) { //右下
                    if(!check(color, num[row][column], big)) {
                        sumpart++;
                    }
                }
            }
            if(sumpart == 8) {
                int cishu = 0;
                for(int a = 1; a <= n; a++) {
                    for(int b = 1; b <= m; b++) {
                        if(num[a - 1][b - 1] == color) {
                            cishu++;
                        }
                    }
                }
                if(cishu == 1) {
                    therow = row;
                    thecolumn = column;
                    sum++;
                }
            }
            if((sumpart == 5) && (column == 1 || column == m ||row==1||row==n)) {
                int cishu = 0;
                for(int a = 1; a <= n; a++) {
                    for(int b = 1; b <= m; b++) {
                        if(num[a - 1][b - 1] == color) {
                            cishu++;
                        }
                    }
                }
                if(cishu == 1) {
                    therow = row;
                    thecolumn = column;
                    sum++;
                }
            }
            if(sumpart==3&&(color==num[n-1][0]||color==num[0][0]||color==num[0][m-1]||color==num[n-1][m-1]||n==2)){
                int cishu = 0;
                for(int a = 1; a <= n; a++) {
                    for(int b = 1; b <= m; b++) {
                        if(num[a - 1][b - 1] == color) {
                            cishu++;
                        }
                    }
                }
                if(cishu == 1) {
                    therow = row;
                    thecolumn = column;
                    sum++;
                }
            }
            if(n==1&&sumpart==0&&(color==num[n-1][0]||color==num[0][0]||color==num[0][m-1]||color==num[n-1][m-1])){
                int cishu = 0;
                for(int a = 1; a <= n; a++) {
                    for(int b = 1; b <= m; b++) {
                        if(num[a - 1][b - 1] == color) {
                            cishu++;
                        }
                    }
                }
                if(cishu == 1) {
                    therow = row;
                    thecolumn = column;
                    sum++;
                }
            }
        }
    }
    if(sum > 1) {
        cout << "Not Unique" << endl;
    } else if(sum == 1) {
        printf("(%d, %d): %d", thecolumn, therow, num[therow - 1][thecolumn - 1]);
    } else if(sum == 0) {
        cout << "Not Exist" << endl;
    }
    return 0;
}
```

### 1069 微博转发抽奖
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <vector>
#include <set>

//中奖者之间间隔(n-1)个人

using namespace std;

int main() {
    int m, n, s;
    cin >> m >> n >> s;
    vector<string> name;
    for(int i = 1; i <= m; i++) {
        string str;
        cin >> str;
        name.push_back(str);
    }
    set<string> check;
    vector<string> result;
    if(s <= m) {
        result.push_back(name.at(s - 1));
        check.insert(name.at(s - 1));
        int flag = 1;
        for(int i = s + 1; i <= m; i++) {
            if(flag != n) {
                flag++;
            } else {
                if(check.find(name.at(i - 1)) == check.end()) {
                    result.push_back(name.at(i - 1));
                    flag = 1;
                    check.insert(name.at(i - 1));
                }
            }
        }
        for(auto it = result.begin(); it != result.end(); it++) {
            cout << *it << endl;
        }
    } else {
        cout << "Keep going..." << endl;
    }
    return 0;
}
```

### 1070 结绳
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>

using namespace std;

int main() {
    int n;
    cin >> n;
    float num[n];
    for(int i = 1; i <= n; i++) {
        cin >> num[i - 1];
    }
    sort(num, num + n);
    for(int i = 2; i <= n; i++) {
        num[i - 1] = num[i - 1] / 2 + num[i - 2] / 2;
    }
    printf("%d\n", (int)num[n - 1]);
    return 0;
}
```

### 1071 小赌怡情
```c++
#include <iostream>
#include <stdio.h>

//搞清楚结果数组数字的意义

using namespace std;

int main() {
    int sum, k;
    cin >> sum >> k;
    int have[k] = {0};
    int get[k] = {0};
    int result[k] = {0}; //1获胜，-1失败,3没钱了
    int i;
    for(i = 1; i <= k; i++) {
        int n1, b, t, n2;
        cin >> n1 >> b >> t >> n2;
        if(sum == 0) {
            continue;
        }
        if(t > sum && sum != 0) {
            result[i - 1] = -2;
            have[i - 1] = sum;
        } else {
            if((n2 > n1 && b == 1) || (n1 > n2 && b == 0)) {
                result[i - 1] = 1;
                sum = sum + t;
                have[i - 1] = sum;
                get[i - 1] = t;
            } else if((n2 > n1 && b == 0) || (n1 > n2 && b == 1)) {
                result[i - 1] = -1;
                sum = sum - t;
                get[i - 1] = t;
                have[i - 1] = sum;
            }
        }
    }
    for(int i = 1; i <= k; i++) {
        int theresult = result[i - 1];
        if(theresult == 0) {
            cout << "Game Over." << endl;
            break;
        } else if(theresult == 1) {//获胜
            printf("Win %d!  Total = %d.\n", get[i - 1], have[i - 1]);
        } else if(theresult == -1) {//失败
            printf("Lose %d.  Total = %d.\n", get[i - 1], have[i - 1]);
        } else if(theresult == -2) {//赌资不够
            printf("Not enough tokens.  Total = %d.\n", have[i - 1]);
        }
    }
    return 0;
}
```

### 1072 开学寄语
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <vector>

//使用g++编译器，clang++无法通过
//不必须一定单字符串储存，利用输出样式规划空格位置

using namespace std;

bool check(string str, string ban[], int len) {
    for(int i = 1; i <= len; i++) {
        if(str == ban[i - 1])
            return false;
    }
    return true;
}

int main() {
    int n, m;
    cin >> n >> m;
    string ban[m];
    for(int i = 1; i <= m; i++) {
        cin >> ban[i - 1];
    }
    vector<string> student;
    vector<string> bebans;
    int sum = 0; //总违禁品数
    for(int i = 1; i <= n; i++) {
        string name;
        cin >> name;
        int m;
        cin >> m;
        bool flag = false;//学生是否存在问题
        string bans;
        for(int a = 1; a <= m; a++) {
            string foods;
            cin >> foods;
            if(!check(foods, ban, m)) {
                flag = true;
                bans = bans + ' ' + foods;
                sum++;
            }
        }
        if(flag) {//如果学生存在问题
            student.push_back(name);
            bebans.push_back(bans);
        }
    }
    int len = student.size();
    for(int i = 1; i <= len; i++) {
        cout << student.at(i - 1) << ":" << bebans.at(i - 1) << endl;
    }
    cout << len << " " << sum << endl;
    return 0;
}
```

### 1073 多选题常见计分法
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>

//输出选项错误次数 等于 某个题中所有选项的各自错误次数中最大的那个
//错选和漏选都是错误
//垃圾文案编辑，去吃屎

using namespace std;

struct problem {
    double score;
    int sumchoice;
    int rightchoice;
    string right;
};

struct wrong {
    int id;
    int sum = 0;
    int choice[5] = {0};
};

int cmp(struct wrong a, struct wrong b) {
    return (a.sum != b.sum) ? a.sum > b.sum : a.id < b.id;
}

int main() {
    int n, m;
    cin >> n >> m;
    problem prs[m];
    wrong ps[m];
    int flag = 0;//记录最大的选项错误次数
    for(int i = 1; i <= m; i++) {
        cin >> prs[i - 1].score;
        cin >> prs[i - 1].sumchoice;
        cin >> prs[i - 1].rightchoice;
        ps[i - 1].id = i;
        for(int a = 1; a <= prs[i - 1].rightchoice; a++) {
            char ch;
            cin >> ch;
            prs[i - 1].right += ch;
        }
    }
    double everyscore[n] = {0};
    for(int i = 1; i <= n; i++) {
        for(int a = 1; a <= m; a++) {
            char ch;
            cin >> ch;//吸收左括号
            int sum;
            cin >> sum;
            string answer;
            int re = 1; //表示结果，-1没分，1有分
            int rights = 0; //正确答案个数
            for(int b = 1; b <= sum; b++) {
                cin >> ch;
                int index = prs[a - 1].right.find(ch);
                if(index == -1) {
                    re = -1;
                    ps[a - 1].choice[ch - 'a']++;
                    if(ps[a - 1].choice[ch - 'a'] > flag)
                        flag = ps[a - 1].choice[ch - 'a'];
                } else {
                    rights++;
                    answer += ch;
                }
            }
            int thelen = prs[a - 1].right.size();
            int re2 = 1;
            for(int c = 1; c <= thelen; c++) {
                int index = answer.find(prs[a - 1].right[c - 1]);
                if(index == -1) {
                    ps[a - 1].choice[prs[a - 1].right[c - 1] - 'a']++;
                    re2 = -1;
                    if(ps[a - 1].choice[prs[a - 1].right[c - 1] - 'a'] > flag)
                        flag = ps[a - 1].choice[prs[a - 1].right[c - 1] - 'a'];
                }
            }
            cin >> ch;//吸收右括号
            if(re == 1 && rights == thelen) {
                everyscore[i - 1] += prs[a - 1].score;
            } else if(re != -1) {
                everyscore[i - 1] += prs[a - 1].score * 0.5;
            } else if(re == -1 || re2 == -1) {
                ps[a - 1].sum++;
            }
        }
    }
    for(int i = 1; i <= n; i++) {
        printf("%.1lf\n", everyscore[i - 1]);
    }
    sort(ps, ps + m, cmp);
    int index = 0;
    if(flag == 0) {
        cout << "Too simple" << endl;
    } else {
        while(index!=m) {
            for(int i = 1; i <= 5; i++) {
                if(ps[index].choice[i - 1] == flag) {
                    cout << flag << " " << ps[index].id << "-" << (char)('a' + (i - 1)) << endl;
                }
            }
            index++;
        }
    }
    return 0;
}
```

### 1074 宇宙无敌加法器
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <math.h>
#include <stack>

//注意去除前置0
//补齐字符串位数再运算
//注意结果为0的情况

using namespace std;

int main() {
    string str, str1, str2;
    cin >> str >> str1 >> str2;
    if(str1.size() < str2.size()) {//补齐字符串位数
        int len = str2.size() - str1.size();
        string temp = str1;
        str1 = "";
        for(int i = 1; i <= len; i++) {
            str1 += '0';
        }
        str1 += temp;
    } else if(str1.size() > str2.size()) {
        int len = str1.size() - str2.size();
        string temp = str2;
        str2 = "";
        for(int i = 1; i <= len; i++) {
            str2 += '0';
        }
        str2 += temp;
    }
    int len = str1.size();
    int n = str.size();
    stack<int> result;
    int flag = 0;
    for(int i = len; i >= 1; i--) {
        int ch1 = str1[i - 1] - '0';
        int ch2 = str2[i - 1] - '0';
        int wei = str[n - 1] - '0';
        if(wei == 0) {
            wei = 10;
        }
        result.push((ch1 + ch2 + flag) % wei);
        if(ch1 + ch2 + flag >= wei) {
            flag = (ch1 + ch2 + flag) / wei;
        } else {
            flag = 0;
        }
        n--;
    }
    string re = to_string(flag);//把首位加入
    while(!result.empty()) {
        re += to_string(result.top());
        result.pop();
    }
    int i = 0;
    while(re[i] == '0') {//去除前置0
        i++;
    }
    if(re.substr(i, -1).size() == 0) {//注意单独输出0
        cout << 0 << endl;
    } else {
        cout << re.substr(i, -1) << endl;
    }
    return 0;
}
```

### 1075 ★链表元素分类★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <vector>

//不一定三种情况都有结点对应，注意最后的下标越界问题，套娃越来越大
//静态链表

using namespace std;

struct node {
    int data;
    int next;
};

int main() {
    int first, n, k;
    scanf("%d%d%d", &first, &n, &k);
    node li[100001];
    for(int i = 1; i <= n; i++) {
        int temp;
        scanf("%d", &temp);
        scanf("%d%d", &li[temp].data, &li[temp].next);
    }
    vector<int> ve1;
    vector<int> ve2;
    vector<int> ve3;
    while(first != -1) {
        int thedata = li[first].data;
        if(thedata < 0) {
            ve1.push_back(first);
        } else if(thedata >= 0 && thedata <= k) {
            ve2.push_back(first);
        } else {
            ve3.push_back(first);
        }
        first = li[first].next;
    }
    int len1 = ve1.size();
    for(int i = 1; i <= len1; i++) {
        if(i != len1) {
            printf("%05d %d %05d\n", ve1.at(i - 1), li[ve1.at(i - 1)].data, ve1.at(i));
        } else if(ve2.size() != 0) {
            printf("%05d %d %05d\n", ve1.at(i - 1), li[ve1.at(i - 1)].data, ve2.at(0));
        } else if(ve3.size() != 0) {
            printf("%05d %d %05d\n", ve1.at(i - 1), li[ve1.at(i - 1)].data, ve3.at(0));
        } else {
            printf("%05d %d %d\n", ve1.at(i - 1), li[ve1.at(i - 1)].data, -1);
        }
    }
    int len2 = ve2.size();
    for(int i = 1; i <= len2; i++) {
        if(i != len2) {
            printf("%05d %d %05d\n", ve2.at(i - 1), li[ve2.at(i - 1)].data, ve2.at(i));
        } else if(ve3.size() != 0) {
            printf("%05d %d %05d\n", ve2.at(i - 1), li[ve2.at(i - 1)].data, ve3.at(0));
        } else {
            printf("%05d %d %d\n", ve2.at(i - 1), li[ve2.at(i - 1)].data, -1);
        }
    }
    int len3 = ve3.size();
    for(int i = 1; i <= len3; i++) {
        if(i != len3) {
            printf("%05d %d %05d\n", ve3.at(i - 1), li[ve3.at(i - 1)].data, ve3.at(i));
        } else {
            printf("%05d %d %d\n", ve3.at(i - 1), li[ve3.at(i - 1)].data, -1);
        }
    }
    return 0;
}
```

### 1076 WIFI密码
```c++
#include <iostream>
#include <algorithm>
#include <string>

//注意有的题可能答案不止一个，为多选

using namespace std;

int main() {
    int n;
    cin >> n;
    string result;
    for(int i=1; i<=n; i++) {
        for(int a=1; a<=4; a++) {
            string part;
            cin >> part;
            if(part[2]=='T') {
                int num;
                switch(part[0]) {
                case 'A':
                    num=1;
                    break;
                case 'B':
                    num=2;
                    break;
                case 'C':
                    num=3;
                    break;
                case 'D':
                    num=4;
                    break;
                }
                result+=(num+'0');
            }
        }
    }
    cout << result << endl;
    return 0;
}
```

### 1077 互评成绩计算
```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <math.h>

//能边输入边处理数据最好，提高效率
//★不要使用vector的数组

using namespace std;

int main() {
    int n,m;
    cin >> n >> m;
    float result[n];
    for(int i=1; i<=n; i++) {
        int teacherscore;
        cin >> teacherscore;
        vector<int> ve;
        ve.push_back(teacherscore);
        for(int a=1; a<=n-1; a++) {
            float score;
            cin >> score;
            if(score>=0&&score<=m&&(int)score==score) {
                ve.push_back(score);
            }
        }
        sort(ve.begin()+1,ve.end());
        int len=ve.size();
        float studentscore=0;
        for(int it=3; it<=len-1; it++) {
            studentscore=studentscore+ve.at(it-1);
        }
        studentscore=studentscore/(len-3);
        result[i-1]=(teacherscore+studentscore)/2;
    }
    for(int i=1; i<=n; i++) {
        cout << round(result[i-1]) << endl;
    }
    return 0;
}
```

### 1078 字符串压缩与解压
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>
#include <sstream>

//注意压缩时最后部分的处理
//解压时数字不一定是个位数

using namespace std;

string compress(string str) {
    int len = str.size();
    string result;
    for(int i = 1; i <= len; i++) {
        int begins = i;
        for(int ends = i; ends <= len; ends++) {
            if((str[ends - 1] != str[begins - 1])) {
                if(ends - begins < 2) {
                    result += str[begins - 1];
                } else {
                    result += to_string(ends - begins) + str[begins - 1];
                }
                i = ends - 1;
                break;
            }
            if(ends == len) {
                if(ends - begins == 0) {
                    result += str[begins - 1];
                } else {
                    result += to_string(ends - begins + 1) + str[ends - 1];
                }
                i = len + 1;
            }
        }
    }
    return result;
}

string decompression(string str) {
    int len = str.size();
    string result;
    for(int i = 1; i <= len; i++) {
        if(isdigit(str[i - 1])) {
            string strnum;
            while(isdigit(str[i - 1])) {
                strnum += str[i - 1];
                i++;
            }
            stringstream ss;
            ss << strnum;
            int num;
            ss >> num;
            for(int a = 1; a <= num; a++) {
                result += str[i - 1];
            }
        } else {
            result += str[i - 1];
        }
    }
    return result;
}

int main() {
    char choice;
    cin >> choice;
    getchar();
    string str;
    getline(cin, str);
    if(choice == 'C')
        cout << compress(str) << endl;
    else if(choice == 'D')
        cout << decompression(str) << endl;
    return 0;
}
```

### 1079 ★延迟的回文数★
```c++
#include <iostream>
#include <algorithm>
#include <string>
#include <sstream>
#include <vector>

//用指针实现了数字字符串相加（只支持正整数）
//先检测是否回文，再运算

using namespace std;

string getre(string str) {
    string result;
    int len = str.size();
    for(int i = len; i >= 1; i--) {
        result += str[i - 1];
    }
    return result;
}

string add(string str1, string str2) {
    int len1 = str1.size();
    int len2 = str2.size();

    int themin = min(len1, len2);
    int themax = max(len1, len2);
    string temp;
    for(int i = 1; i <= themax - themin; i++) {
        temp += '0';
    }
    if(len1 == themin) {
        string change = str1;
        str1 = "";
        str1 = temp + change;
    } else {
        string change = str2;
        str2 = "";
        str2 = temp + change;
    }

    vector<int> ve;
    int len = str1.size();
    for(int i = 1; i <= len; i++) {
        int num = (str1[i - 1] - '0') + (str2[i - 1] - '0');
        if(num <= 9 || i == 1) {
            ve.push_back(num);
        } else {
            auto before = ve.end();
into:
            before--;
            (*before)++;
            if(*before > 9 && before != ve.begin()) {
                *before = (*before) % 10;
                goto into;
            }
            ve.push_back(num % 10);
        }
    }
    string result;
    int velen = ve.size();
    for(int i = 1; i <= velen; i++) {
        result += to_string(ve.at(i - 1));
    }
    return result;
}

bool checkre(string str) {
    string str2 = getre(str);
    if(str == str2)
        return true;
    else
        return false;
}

int main() {
    string str1;
    cin >> str1;
    int i;
    for(i = 1; i <= 10; i++) {
        if(checkre(str1)) {
            cout << str1 << " is a palindromic number." << endl;
            break;
        }
        string str2 = getre(str1);
        string result = add(str1, str2);
        cout << str1 << " + " << str2 << " = " << result << endl;
        str1 = result;
    }
    if(i > 10) {
        cout << "Not found in 10 iterations." << endl;
    }
    return 0;
}
```

### 1080 ★MOOC期终成绩★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <map>
#include <math.h>
#include <set>

//思路同1015
//但中间多了一步简单转换
//注意超时问题，输入尽量scanf，输出尽量printf

using namespace std;

struct student {
    string id;
    float isp = -1;
    float mid = -1;
    float finaly = -1;
    int sum = -1;
};

struct sortstudent {
    bool operator() (const student & a, const student & b) const {
        if(a.sum != b.sum)
            return a.sum > b.sum;
        else
            return a.id < b.id;
    }
};

int compare(int p, int m, int n) {
    int temp = max(p, m);
    int result = max(temp, n);
    if(result == p) {
        return 1;
    } else if(result == m) {
        return 2;
    } else {
        return 3;
    }
}

int main() {
    int p, m, n;
    cin >> p >> m >> n;
    map<string, float> pscore;
    for(int i = 1; i <= p; i++) {
        char s[21];
        scanf("%s", s);
        getchar();
        float score;
        scanf("%f", &score);
        getchar();
        pscore[s] = score;
    }
    map<string, float> midscore;
    for(int i = 1; i <= m; i++) {
        char s[21];
        scanf("%s", s);
        getchar();
        float score;
        scanf("%f", &score);
        getchar();
        midscore[s] = score;
    }
    map<string, float> finscore;
    for(int i = 1; i <= n; i++) {
        char s[21];
        scanf("%s", s);
        getchar();
        float score;
        scanf("%f", &score);
        getchar();
        finscore[s] = score;
    }
    int len = compare(p, m, n);
    map<string, float> themax;
    if(len == 1) {
        themax = pscore;
    } else if(len == 2) {
        themax = midscore;
    } else {
        themax = finscore;
    }
    len = themax.size();
    set<student, sortstudent> result;
    for(auto it = themax.begin(); it != themax.end(); it++) {
        auto it1 = pscore.find(it->first);
        auto it2 = midscore.find(it->first);
        auto it3 = finscore.find(it->first);
        if(it1 != pscore.end() && it2 != midscore.end() && it3 != finscore.end()) {
            if(it1->second >= 200 && it2->second > it3->second) {
                student part;
                part.id = it->first;
                part.isp = it1->second;
                part.mid = it2->second;
                part.finaly = it3->second;
                part.sum = round(part.mid * 0.4 + part.finaly * 0.6);
                if(part.sum >= 60)
                    result.insert(part);
            } else if(it1->second >= 200 && it2->second <= it3->second) {
                student part;
                part.id = it->first;
                part.isp = it1->second;
                part.mid = it2->second;
                part.finaly = it3->second;
                part.sum = round(part.finaly);
                if(part.sum >= 60)
                    result.insert(part);
            }
        } else if(it1 != pscore.end() && it2 == midscore.end() && it3 != finscore.end()) {
            if(it1->second >= 200) {
                student part;
                part.id = it->first;
                part.isp = it1->second;
                part.finaly = it3->second;
                part.sum = round(part.finaly);
                if(part.sum >= 60)
                    result.insert(part);
            }
        }
    }
    for(set<student>::iterator it = result.begin(); it != result.end(); it++) {
        cout << (*it).id;
        printf(" %.0f %.0f %.0f %d\n", (*it).isp, (*it).mid, (*it).finaly, (*it).sum);
    }
    return 0;
}
```

### 1081 检查密码
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <string>

//注意结果实数的实际意义

using namespace std;

int check(string str) {
    bool num = false;
    bool letter = false;
    bool legal = true;
    int len = str.size();
    for(int i = 1; i <= len; i++) {
        char ch = str[i - 1];
        if((ch >= 'A' && ch <= 'Z') || (ch >= 'a' && ch <= 'z')) {
            letter = true;
        } else if(ch >= '0' && ch <= '9') {
            num = true;
        } else if(ch == '.') {
            continue;
        } else {
            legal = false;
            break;
        }
    }
    if(!legal) {
        return -2;
    } else if(!num && letter) {
        return -1;
    } else if(num && !letter) {
        return 1;
    } else {
        return 2;
    }
}

int main() {
    int n;
    cin >> n;
    int result[n] = {0}; //0太短，1需要字母，-1需要数字，-2存在不合法字符,2完美
    getchar();
    for(int i = 1; i <= n; i++) {
        string str;
        getline(cin, str);
        if(str.size() >= 6) {
            result[i - 1] = check(str);
        }
    }
    for(int i = 1; i <= n; i++) {
        int theresult = result[i - 1];
        if(theresult == 0) {
            cout << "Your password is tai duan le." << endl;
        } else if(theresult == -2) {
            cout << "Your password is tai luan le." << endl;
        } else if(theresult == 1) {
            cout << "Your password needs zi mu." << endl;
        } else if(theresult == -1) {
            cout << "Your password needs shu zi." << endl;
        } else {
            cout << "Your password is wan mei." << endl;
        }
    }
    return 0;
}
```

### 1082 射击比赛
```c++
#include <iostream>
#include <algorithm>
#include <map>
#include <iterator>

//搞清楚迭代器使用时的指针指向
//迭代器指针只能进行++和--运算，不能一次加或减多个
//map容器排列的根据是第一个元素

using namespace std;

int main() {
    int n;
    cin >> n;
    map<int,string> id;
    for(int i=1; i<=n; i++) {
        string name;
        cin >> name;
        int x;
        int y;
        cin >> x >> y;
        id[x*x+y*y]=name;
    }
    map<int,string>::iterator it=id.begin();
    cout << it->second << " ";
    it=--id.end();
    cout << it->second << endl;
    return 0;
}
```

### 1083 是否存在相等的差
```c++
#include <iostream>
#include <algorithm>
#include <math.h>

//注意数组索引的意义

using namespace std;

int main() {
    int n;
    cin >> n;
    int num[n];
    int sum[n+1]={0};
    for(int i=1;i<=n;i++){
        cin >> num[i-1];
        int index=fabs(num[i-1]-i);
        sum[index]++;
    }
    for(int i=n+1;i>=1;i--){
        if(sum[i-1]>1){
            cout << i-1 << " " << sum[i-1] << endl;
        }
    }
    return 0;
}
```

### 1084 外观数列
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>

//外观数列下一个位数字+个数
//字符串最后一位为'\0'，不用担心越界

using namespace std;

string getnext(string str) {
    string re;
    int len = str.size();
    for(int i = 1; i <= len; i++) {
        char ch = str[i - 1];
        for(int a = i; a <= len + 1; a++) {
            if(str[a - 1] != ch) {
                re += ch + to_string(a - i);
                i = a - 1; //注意大循环每次结束的i++
                break;
            }
        }
    }
    return re;
}

int main() {
    string d;
    int n;
    cin >> d >> n;
    for(int i = 1; i <= n - 1; i++) {
        d = getnext(d);
    }
    cout << d << endl;
    return 0;
}
```

### 1085 ★PAT单位排行★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>
#include <iterator>
#include <set>
#include <vector>

//一个学校的分数正常运算结束后，再取整数进行b排名
//注意并列排名的排名顺序
//思路同1015
//800ms随便造

using namespace std;

struct school {
    string id;
    float score = 0;
    int people = 0;
};

void tolowerletter(string::iterator begins, string::iterator ends) {
    while(begins != ends) {
        if(*begins >= 'A' && *begins <= 'Z') {
            *begins += 32;
        }
        begins++;
    }
}

struct sortschool {
    bool operator () (const school& a, const school& b) const {
        if(a.score != b.score)
            return a.score > b.score;
        else if(a.score == b.score && a.people != b.people)
            return a.people < b.people;
        else
            return a.id < b.id;
    }
};

int main() {
    int n;
    cin >> n;
    set<string> test;
    vector<school> ve;
    for(int i = 1; i <= n; i++) {
        string studentid;
        float studentscore;
        string studentchool;
        cin >> studentid >> studentscore >> studentchool;
        school part;
        tolowerletter(studentchool.begin(), studentchool.end());
        if(studentid[0] == 'B') {
            studentscore = studentscore / 1.5;
        } else if(studentid[0] == 'A') {
            studentscore = studentscore;
        } else if(studentid[0] == 'T') {
            studentscore = studentscore * 1.5;
        }
        set<string>::iterator it = test.find(studentchool);
        if(it == test.end()) {//该学校未添加
            test.insert(studentchool);
            part.id = studentchool;
            part.score += studentscore;
            part.people++;
            ve.push_back(part);
        } else { //该学校已添加
            for(vector<school>::iterator it2 = ve.begin(); it2 != ve.end(); it2++) {
                if((*it2).id == studentchool) {
                    school newschool = *it2;
                    newschool.score += studentscore;
                    newschool.people++;
                    ve.erase(it2);
                    ve.push_back(newschool);
                    break;
                }
            }
        }
    }

    set<school, sortschool> result;
    for(auto it = ve.begin(); it != ve.end(); it++) {
        school part = *it;
        part.score = (int)part.score;
        result.insert(part);
    }
    int flag = 1;
    int counts = 0;
    cout << result.size() << endl;
    for(auto it = result.begin(); it != result.end();) {
        cout << flag << " ";
        cout << (*it).id << " " << (int)((*it).score) << " " << (*it).people << endl;
        counts++;
        auto before = it;
        auto after = ++it;
        if(after != result.end() && (*before).score != (*after).score) {
            flag = counts + 1;
        }
    }
    return 0;
}
```

### 1086 就不告诉你
```c++
#include <iostream>
#include <string>
#include <sstream>

//注意结果末尾为0，输出时需要舍弃

using namespace std;

int main() {
    int a,b;
    cin >> a >> b;
    string str=to_string(a*b);
    string result;
    int len=str.size();
    for(int i=len; i>=1; i--) {
        result+=str[i-1];
    }
    int num=stoi(result);
    cout << num << endl;
    return 0;
}
```

### 1087 有多少不同的值
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>
#include <set>

using namespace std;

int main() {
    int n;
    cin >> n;
    set<int> num;
    for(int i = 1; i <= n; i++) {
        num.insert(i / 2 + i / 3 + i / 5);
    }
    cout << num.size() << endl;
    return 0;
}
```

### 1088 三人行
```c++
#include <iostream>

//丙能力值不一定是整数
//函数传参数会自动兼容变化

using namespace std;

string pk(int a, float b) {
    if(a > b)
        return "Gai";
    else if(a == b)
        return "Ping";
    else
        return "Cong";
}

int main() {
    int m, x, y;
    cin >> m >> x >> y;
    int a;
    for(a = 99; a >= 10; a--) {
        int b = a % 10 * 10 + a / 10;
        float c = b / (float)y;
        if((a - b) * (a - b) == x * x * c * c && y * c == b) {
            cout << a << " " << pk(m, a) << " " << pk(m, b) << " " << pk(m, c) << endl;
            break;
        }
    }
    if(a == 9)
        cout << "No Solution" << endl;
    return 0;
}
```

### 1089 狼人杀-简单版
```c++
#include <iostream>
#include <stdio.h>
#include <algorithm>

//假设两个狼人，判断是否符合条件
//条件是狼人只有一个人撒谎，村民只有一个人撒谎

using namespace std;

bool check(int a, int b, int num[], int n) {
    int sum = 0;
    n++;
    for(int i = 1; i <= n; i++) {
        if(i != a && i != b) {
            if(num[i] > 0 && (num[i] == a || num[i] == b)) {
                sum++;
            } else if(num[i] < 0 && (-num[i] != a && -num[i] != b)) {
                sum++;
            }
        }
    }
    if(sum == 1)
        return true;
    else
        return false;
}

int main() {
    int n;
    cin >> n;
    int num[n + 1];
    for(int i = 1; i <= n; i++) {
        cin >> num[i];
    }
    for(int a = 1; a <= n - 1; a++) {
        for(int b = a + 1; b <= n; b++) {
            if(find(num, num + n + 1, -a) != num + n || find(num, num + n + 1, -b) != num + n) {
                if(check(a, b, num, n + 1)) {
                    if(num[a] > 0 && (num[a] == a || num[a] == b)) {
                        if(num[b] > 0 && (num[b] != a && num[b] != b)) {
                            cout << a << " " << b << endl;
                            return 0;
                        } else if(num[b] < 0 && (-num[b] == a || -num[b] == b)) {
                            cout << a << " " << b << endl;
                            return 0;
                        }
                    } else if(num[a] < 0 && -num[a] != a && -num[a] != b) {
                        if(num[b] > 0 && (num[b] != a && num[b] != b)) {
                            cout << a << " " << b << endl;
                            return 0;
                        } else if(num[b] < 0 && (-num[b] == a || -num[b] == b)) {
                            cout << a << " " << b << endl;
                            return 0;
                        }
                    }
                    if(num[b] > 0 && (num[b] == a || num[b] == b)) {
                        if(num[a] > 0 && (num[a] != a && num[a] != b)) {
                            cout << a << " " << b << endl;
                            return 0;
                        } else if(num[a] < 0 && (-num[a] == a || -num[a] == b)) {
                            cout << a << " " << b << endl;
                            return 0;
                        }
                    } else if(num[b] < 0 && -num[b] != a && -num[b] != b) {
                        if(num[a] > 0 && (num[a] != a && num[a] != b)) {
                            cout << a << " " << b << endl;
                            return 0;
                        } else if(num[a] < 0 && (-num[a] == a || -num[a] == b)) {
                            cout << a << " " << b << endl;
                            return 0;
                        }
                    }
                }
            }
        }
    }
    cout << "No Solution" << endl;
    return 0;
}
```

### 1090 危险品装箱
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <map>
#include <vector>

//注意一种物品可能与多个不相容

using namespace std;

int main() {
    int n, m;
    cin >> n >> m;
    map<string, vector<string>> wrong;
    for(int i = 1; i <= n; i++) {
        string str1, str2;
        cin >> str1 >> str2;
        wrong[str1].push_back(str2);
        wrong[str2].push_back(str1);
    }
    int result[m] = {0}; //1可以，-1不可以
    for(int i = 1; i <= m; i++) {
        int sum;
        cin >> sum;
        vector<string> foods;
        int flag = 1;
        for(int a = 1; a <= sum; a++) {
            string str;
            cin >> str;
            foods.push_back(str);
        }
        for(int a = 1; a <= sum; a++) {
            if(wrong[foods.at(a - 1)].size() != 0) {
                vector<string> thewrong = wrong[foods.at(a - 1)];
                for(int b = 1; b <= sum; b++) {
                    vector<string>::iterator it2 = find(thewrong.begin(), thewrong.end(), foods.at(b - 1));
                    if(it2 != thewrong.end()) {
                        flag = -1;
                        goto wancheng;
                    }
                }
            }
        }
wancheng:
        result[i - 1] = flag;
    }
    for(int i = 1; i <= m; i++) {
        if(result[i - 1] == -1)
            cout << "No" << endl;
        else
            cout << "Yes" << endl;
    }
    return 0;
}
```

### 1091 N-自守数
```c++
#include <iostream>
#include <algorithm>

//注意截取的位置

using namespace std;

int main() {
    int m;
    cin >> m;
    int num[m];
    for(int i=1; i<=m; i++) {
        cin >> num[i-1];
    }
    for(int i=1; i<=m; i++) {
        int n;
        for(n=1; n<10; n++) {
            int result=n*num[i-1]*num[i-1];
            string str1=to_string(num[i-1]);
            string str2=to_string(result);
            int len1=str1.size();
            int len2=str2.size();
            if(str2.substr(len2-len1,len1)==str1) {
                cout << n << " " << result << endl;
                break;
            }
        }
        if(n==10) {
            cout << "No" << endl;
        }
    }
    return 0;
}
```

### 1092 最好吃的月饼
```c++
#include <iostream>
#include <vector>

//注意行数和列数别乱套

using namespace std;

int main() {
    int n,m;
    cin >> n >> m;
    int num[m][n];
    for(int row=1; row<=m; row++) {
        for(int column=1; column<=n; column++) {
            cin >> num[row-1][column-1];
        }
    }
    int sum[n]= {0};
    for(int i=1; i<=n; i++) {
        for(int row=1; row<=m; row++) {
            sum[i-1]=sum[i-1]+num[row-1][i-1];
        }
    }
    int max=sum[0];
    for(int i=2; i<=n; i++) {
        if(sum[i-1]>max) {
            max=sum[i-1];
        }
    }
    cout << max << endl;
    vector<int> ve;
    for(int i=1; i<=n; i++) {
        if(sum[i-1]==max) {
            ve.push_back(i);
        }
    }
    int len=ve.size();
    for(int i=1; i<=len; i++) {
        cout << ve.at(i-1);
        if(i!=len) {
            cout << " ";
        }
    }
    return 0;
}
```

### 1093 字符串A+B
```c++
#include <iostream>
#include <algorithm>
#include <string>
#include <set>

//注意set会自动排序，必须导入头文件#include <set>

using namespace std;

int main() {
    string str1;
    string str2;
    getline(cin,str1);
    getline(cin,str2);
    string str=str1+str2;
    int len=str.size();
    set<char> se;
    string result;
    for(int i=1;i<=len;i++){
        int begin=se.size();
        char ch=str[i-1];
        se.insert(ch);
        int end=se.size();
        if(end!=begin){
            result+=ch;
        }
    }
    cout << result << endl;
    return 0;
}
```

### 1094 谷歌的招聘
```c++
#include <iostream>
#include <stdio.h>
#include <string>
#include <algorithm>
#include <math.h>
#include <sstream>

//素数的判断注意0和1
//输出的数必须满足位数，字符串末端不满足位数的不考虑

using namespace std;

bool ifvegetable(int m) {
    if(m==0||m==1)
        return false;
    for(int i=2; i<=sqrt(m); i++) {
        if(m%i==0) {
            return false;
        }
    }
    return true;
}

int main() {
    int n,k;
    cin >> n >> k;
    string str;
    cin >> str;
    bool flag=false;
    for(int i=1; i<=n-k+1; i++) {
        string thestr;
        thestr=str.substr(i-1,k);
        int num;
        stringstream ss;
        ss << thestr;
        ss >> num;
        if(ifvegetable(num)) {
            cout << thestr << endl;
            flag=true;
            break;
        }
    }
    if(!flag) {
        cout << "404" << endl;
    }
    return 0;
}
```

### 1095 ★解码PAT准考证★
```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>
#include <string>
#include <set>
#include <vector>
#include <sstream>
#include <map>

//string使用c_str()便可以转换为字符串数组，使用%s输出，提高效率
//边输入便处理数据，不然超时

using namespace std;

struct student {
    string id ;
    int score;
    string level;
    string examroom;
    string examdate;
};

struct room {
    string theroom ;
    int people = 0;
    int sumscore=0;
};

struct sortstudent {
    bool operator() (const student&a, const student&b) const {
        return (a.score != b.score) ? a.score > b.score : a.id < b.id;
    }
};

struct sortroom {
    bool operator() (const room&a, const room&b) const {
        return (a.people != b.people) ? a.people > b.people : a.theroom < b.theroom;
    }
};

int main() {
    int n, m;
    scanf("%d%d", &n, &m);
    set<student, sortstudent> name;
    set<student, sortstudent> nameT;
    set<student, sortstudent> nameA;
    set<student, sortstudent> nameB;
    map<string,room> rooms;//普通分教室
    map<string,map<string,room>> rooms2;//日期分教室
    for(int i = 1; i <= n; i++) {
        char s[20];
        scanf("%s", s);
        getchar();
        student part;
        part.id = s;
        scanf("%d", &part.score);
        part.level = part.id.substr(0, 1);
        part.examroom = part.id.substr(1, 3);
        part.examdate = part.id.substr(4, 6);
        name.insert(part);
        if(part.level=="T"){
            nameT.insert(part);
        }else if(part.level=="A"){
            nameA.insert(part);
        }else if(part.level=="B"){
            nameB.insert(part);
        }

        rooms[part.examroom].theroom=part.examroom;
        rooms[part.examroom].people+=1;
        rooms[part.examroom].sumscore+=part.score;

        (rooms2[part.examdate])[part.examroom].theroom=part.examroom;
        (rooms2[part.examdate])[part.examroom].people+=1;
        (rooms2[part.examdate])[part.examroom].sumscore+=part.score;
    }
    vector<string> orders;
    set<student,sortstudent> result1[m];
    string result2[m];
    set<room, sortroom> result3[m];
    for(int i = 1; i <= m; i++) {
        char s1[2];
        scanf("%s", s1);
        getchar();
        string point = s1;
        if(point == "1") {
            char s2[20];
            scanf("%s", s2);
            getchar();
            string thelevel = s2;
            if(thelevel=="T"){
                result1[i-1]=nameT;
            }else if(thelevel=="A"){
                result1[i-1]=nameA;
            }else if(thelevel=="B"){
                result1[i-1]=nameB;
            }
            string theorder = point + " " + thelevel;
            orders.push_back(theorder);
        } else if(point == "2") {
            char s2[20];
            scanf("%s", s2);
            getchar();
            string theexamroom = s2;
            result2[i - 1] = to_string(rooms[theexamroom].people) + " " + to_string(rooms[theexamroom].sumscore);
            string theorder = point + " " + theexamroom;
            orders.push_back(theorder);
        } else if(point == "3") {
            char s2[20];
            scanf("%s", s2);
            getchar();
            string thedate = s2;
            for(map<string,room>::iterator it=rooms2[thedate].begin();it!=rooms2[thedate].end();it++){
                result3[i-1].insert(it->second);
            }
            string theorder = point + " " + thedate;
            orders.push_back(theorder);
        }
    }
    for(int i = 1; i <= m; i++) {
        cout << "Case " << i << ": " << orders.at(i - 1) << endl;
        char theorder = orders.at(i - 1)[0];
        if(theorder == '1') {
            if(result1[i - 1].size() == 0) {
                printf("NA\n");
                continue;
            } else {
                for(set<student>::iterator it = result1[i - 1].begin(); it != result1[i - 1].end(); it++) {
                    printf("%s %d\n",(*it).id.c_str(),(*it).score);
                }
            }
        } else if(theorder == '2') {
            if(result2[i - 1][0] == '0') {
                printf("NA\n");
                continue;
            } else
                printf("%s\n",result2[i-1].c_str());
        } else if(theorder == '3') {
            if(result3[i - 1].size() == 0) {
                printf("NA\n");
                continue;
            } else {
                for(set<room>::iterator it = result3[i - 1].begin(); it != result3[i - 1].end(); it++) {
                    printf("%s %d\n",(*it).theroom.c_str(),(*it).people);
                }
            }
        }
    }
    return 0;
}
```