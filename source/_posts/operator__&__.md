title:first try
输入输出流（<<.>>）只能使用全局函数的方法进行重载，因为out属于ostream类而前面的ostream类无法找到其原函数

```
std::ostream & operator<<(std::ostream &out,Complex c1)
//定义两个参数是因为<<是双目运算符
{
	out<<c1.a<<"+"<<c1.b<<"i"<<std::endl;//这个里面的<<是系统自带的那个<<
	return out; //避免实现连续输出流
}

```
cin是istream类的对象，cout是ostream类的对象

```
#include<iostream>

class Complex
{
private:
	int a;
	int b;
public:
	friend std::ostream& operator<<(std::ostream &out,Complex c1);
	Complex (int a=0,int b=0)
	{
		this->a=a;
		this->b=b;
	}
};
//用全局函数实现 << 操作符的重载
std::ostream & operator<<(std::ostream &out,Complex c1)//定义两个参数是因为<<是双目运算符
{
	out<<c1.a<<"+"<<c1.b<<"i"<<std::endl;
	return out;
}
void main()
{
	Complex d1(1,2);
	//<<操作符的结合顺序左边大于右边，所以在执行时要看要看两边的数据是否匹配
	//std::cout<<d1<<std::endl是错的，因为执行完std::cout << d1之后，那个函数返回为空，如果返回一个OUT就对了
	std::cout << d1 <<std::endl;
	system("pause");
	return ;
}
```

