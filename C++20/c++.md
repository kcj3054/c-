# auto, decltype

```c++
#include <iostream>
#include <vector>

using namespace std;

void ex5()
{
	int i = 42;
	auto&& ri_1 = i; // l - value..
	auto&& ri_2 = 42; // r - value..
}

template<typename T, typename S>
void func_ex7(T lhs, S rhs)
{
	auto prod1 = lhs * rhs;

	//decltype 값을 받아서 컴파일 타임에 타입을 추론한다 
	typedef decltype(lhs* rhs) product_type; // decltype은 계산을 하지 않고 추론까지한다 
	product_type prod2 = lhs * rhs;

	//decltype(lhs * rhs) prod3 = lhs * rhs
	// decltype prod3 = lhs * rhs
}

//decltype auto와 다르다.. 선언이 된 타입을 그대로 가져온다. 
// trailing return type.. -> auto키워드로 정의된 함수의 반환형을 명시적으로 알려줌.
template<typename T, typename S>
auto func_ex8(T lhs, S rhs) -> decltype(lhs* rhs)
{
	return lhs * rhs;
}

//서로 다른 타입일 때 min을 구현 
template<typename T, typename S>
auto fpmin_wrong(T x, S y) -> decltype(x < y ? x : y)
{
	return x < y ? x : y
}


int main()
{
	auto res = func_ex8(2, 2.2);
	cout << res << endl;

	{
		std::vector<int> vect = { 42,  43 };

		auto first_element = vect[0]; // first_element가 int로
		decltype(vect[1]) second_element = vect[1]; // int& 왜 vec[]의 return type이 &라서.
	}

	{
		
	}
	return 0;
}
```