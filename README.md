# -ArithmeticV1.0
v1.0版 对运算功能进行了完善

/**
*程序功能：没有实现中文或英文或日文的选择。
*            倒计时功能（这个功能我百度了一下  需要windows编程 和 多线程技术支持*实力不够 做不出来  我把它改成了一个记录答题时间）
*程序功能：实现了 判断对错 累计分数 记录答题时间（秒为单位）
*         支持多个运算符 支持括号
*         具体生成算数 是采用的switch分支结构
*
*/

#include<windows.h>
#include <algorithm> 
#include<iostream>
#include<cstdlib>
#include<ctime>
using namespace std;
float Practice();
float Addtion();
float Subtract();
float Multiply();
float Modulo();
void menu();
int main()
{
	int count = 0;
	int right = 0;
	int wrong = 0;
	cout.setf(ios::fixed);
	cout.precision(2);
	srand((unsigned)time(NULL));
	float answer,write=0.00;
	int check = 1;

	while (check)
	{	
		//	声明DWORD变量 记录时间
		DWORD dwStart;
		DWORD dwEnd;
		DWORD useTime;
		int choice;
		menu();
		cin >> choice;
		switch (choice)
		{
		case 1:
			answer = Addtion();
			break;
		case 2:
			answer = Subtract();
			break;
		case 3:
			answer = Multiply();
			break;
		case 4:
			answer = Modulo();
			break;
		case 5:		
			answer = Practice();
			break;
		default:
			break;
		}
		//	使用GetTickCount（）来获取时间
		dwStart = GetTickCount();
		cin >> write;
		dwEnd = GetTickCount();		
		useTime = dwEnd - dwStart;
		cout << "答题时间为："<< useTime/1000 <<"s"<< endl;
		if (write == answer)
			{
				right++;
				cout << "回答正确。" <<endl
					<<"回答问题总分为 "<<++count<<" 回答正确分数为 "<<
					right<<" 错误分数为 "<<wrong<< endl;								
			}
		else
			{
			wrong++;
				cout << "回答错误。" << endl
					<< "回答问题总分为 " << ++count << " 回答正确分数为 " <<
					right << " 错误分数为 " << wrong << endl;
				cout << "正确答案为："<<answer<<endl;
			}	
			
		cout << "继续做题请按1, 退出请按0"<<endl;
		cin >> check;
	}
	system("pause");
	return 0;
}
float Practice()
{
	int range;
	cout << "请输入多少数以内的四则运算：";
	cin >> range;
	cout << endl;
	int a[4] = { 0 };
	srand((unsigned)time(NULL));//	根据系统时间生成随机数
	for (int i = 0; i < 4; i++)
		a[i] = (rand() % range) + 1;
	sort(a,a+4);	//	将数组进行升序排列
	cout << "请输入答案。(小数精确到后2位！)" << endl;
	switch ((rand() % 16) + 1)
	{
	case 1:
		cout << a[0]<< "*"<< a[1] <<"=" ;
		return a[0] * a[1];
	case 2:
		cout << a[0] << "+" << a[1] << "=";
		return a[0] + a[1];
	case 3:
		cout << a[0] << "-" << a[1] << "=";
		return a[0] - a[1];
	case 4:
		cout << a[0] << "/" << a[1] << "=";
		return (a[0] / (a[1]*1.0));
	case 5:
		cout << "(" << a[0] << "/" << a[1] << "+" << a[2] << ")" << "*" << a[3] << "=";
		return (a[0] / (a[1] * 1.0) + a[2]) * a[3];
	case 6:
		cout << "(" << a[0] << "-" << a[1] << "+" << a[2] << ")" << "/" << a[3] << "=";
		return (a[0] - a[1] + a[2]) /a[3];
	case 7:
		cout << a[0] << "/" << a[1] << "+" << a[2] << "*" << a[3] << "=";
		return a[0] / (a[1] * 1.0) + a[2] * a[3];
	case 8:
		cout << a[0] << "+" << a[1] << "+" << a[2] << "*" << a[3] << "=";
		return a[0] + a[1] + a[2] * a[3];
	case 9:
		cout << a[2] << "-" << a[1] << "+" << a[2] << "*" << a[3] << "=";
		return a[2] - a[1] + a[2] * a[3];
	case 10:
		cout << a[0] << "+" << a[1] << "-" << a[2] << "=";
		return a[0] + a[1] - a[2];
	case 11:
		cout << a[0] << "*" << a[1] << "-" << a[2] << "=";
		return a[0] * a[1] - a[2];
	case 12:
		cout << a[0] << "*" << a[1] << "/" << a[2] << "=";
		return a[0] * a[1] / (a[2]*1.0);
	case 13:
		cout << a[0] << "*" << a[1] << "*" << a[2] << "=";
		return a[0] * a[1] * a[2];
	case 14:
		cout << "(" << a[0] << "-" << a[1] << ")" << "*" << " (" << a[2] << "/" << a[3] << ")" << "=";
		return (a[0] - a[1]) * (a[2] / (a[3]*1.0));
	case 15:
		cout << a[0] << " /" << a[1] << "+" << a[2] << "/" << a[3] << "=";
		return a[0] / (a[1]*1.0) + a[2] / (a[3]*1.0);
	case 16:
		cout << "(" << a[0] << " /" << a[1] << "+" << a[2] << ")" << "/" << a[3] << "=";
		return (a[0] / (a[1] * 1.0) + a[2]) / (a[3] * 1.0);
	default:
		cout << a[0] << "+" << a[1] << "=";
		return a[0] + a[1];

	}
}
float Addtion()
{
	int range;
	cout << "请输入多少数以内的四则运算：";
	cin >> range;
	cout << endl;
	int a[4] = { 0 };
	srand((unsigned)time(NULL));//	根据系统时间生成随机数
	for (int i = 0; i < 4; i++)
		a[i] = (rand() % range) + 1;
	sort(a, a + 4);	//	将数组进行升序排列
	cout << "请输入答案。(小数精确到后2位！)" << endl;
	switch ((rand() % 9) + 1)
	{
	case 1:
		cout << a[0] << "+" << a[1] << "=";
		return a[0] + a[1];
	case 2:
		cout << a[3] << "+" << a[1] <<"+"<<a[2]<< "=";
		return a[3] + a[1]+a[2];
	case 3:
		cout << a[3] << "+" << a[1] << "=";
		return a[3] + a[1];
	case 4:
		cout << a[4] << "+" << a[1] << "+"<<a[2]<<"+"<<a[3]<<"=";
		return a[4]+a[3]+a[2]+a[1];
	case 5:
		cout << a[0] << "+" << a[1] << "+" << a[2] << "+" << a[3] << "=";
		return a[0] + a[1] + a[2] + a[3];
	case 6:
		cout << a[3] << "+" << a[1] << "+" << a[2] << "+"<< a[2] << "=";
		return a[3] + a[1] + a[2] + a[2];
	case 7:
		cout << a[0] << "+" << a[1] << "+" << a[3]<<"/"<<a[3] << "+" << a[3] << "=";
		return a[0] + a[1] + a[3]/a[3] + a[3];
	case 8:
		cout << a[0] << "+" << a[1] << "+" << a[2] << "+" << a[3] << "=";
		return a[0] + a[1] + a[2] + a[3];
	case 9:
		cout << a[2] << "+" << a[1]<<"/"<<a[3] << "+" << a[2] << "+" << a[3] << "=";
		return a[2] + a[1]/a[3] + a[2] + a[3];
	default:
		cout << a[0]<<"/"<<a[3] << "+" << a[1] << "=";
		return a[0]/a[3] + a[1];

	}
}
float Subtract()
{
	int range;
	cout << "请输入多少数以内的四则运算：";
	cin >> range;
	cout << endl;
	int a[4] = { 0 };
	srand((unsigned)time(NULL));//	根据系统时间生成随机数
	for (int i = 0; i < 4; i++)
		a[i] = (rand() % range) + 1;
	sort(a, a + 4);	//	将数组进行升序排列
	cout << "请输入答案。(小数精确到后2位！)" << endl;
	switch ((rand() % 9) + 1)
	{
	case 1:
		cout << a[0] << "-" << a[1] << "=";
		return a[0] - a[1];
	case 2:
		cout << a[3] << "-" << a[1] << "-" << a[2] << "=";
		return a[3] - a[1] - a[2];
	case 3:
		cout << a[3] << "-" << a[1] << "=";
		return a[3] - a[1];
	case 4:
		cout << a[4] << "-" << a[1] << "-" << a[2] << "-" << a[3] << "=";
		return a[4] - a[3] - a[2] - a[1];
	case 5:
		cout << a[0] << "-" << a[1] << "-" << a[2] << "-" << a[3] << "=";
		return a[0] - a[1] - a[2] - a[3];
	case 6:
		cout << a[3] << "-" << a[1] << "-" << a[2] << "-" << a[2] << "=";
		return a[3] - a[1] - a[2] - a[2];
	case 7:
		cout << a[0] << "-" << a[1] << "-" << a[3] << "/" << a[3] << "-" << a[3] << "=";
		return a[0] - a[1] - a[3] / a[3] - a[3];
	case 8:
		cout << a[0] << "-" << a[1] << "-" << a[2] << "-" << a[3] << "=";
		return a[0] - a[1] - a[2] - a[3];
	case 9:
		cout << a[2] << "-" << a[1] << "/" << a[3] << "-" << a[2] << "-" << a[3] << "=";
		return a[2] - a[1] / a[3] - a[2] - a[3];
	default:
		cout << a[0] << "/" << a[3] << "-" << a[1] << "=";
		return a[0] / a[3] - a[1];

	}
}
float Modulo()
{
	int range;
	cout << "请输入多少数以内的四则运算：";
	cin >> range;
	cout << endl;
	int a[4] = { 0 };
	srand((unsigned)time(NULL));//	根据系统时间生成随机数
	for (int i = 0; i < 4; i++)
		a[i] = (rand() % range) + 1;
	sort(a, a + 4);	//	将数组进行升序排列
	cout << "请输入答案。(小数精确到后2位！)" << endl;
	switch ((rand() % 4) + 1)
	{
	case 1:
		cout << "(" << a[0] << "/" << a[1] << ")" << "+" << "(" << a[2] << "/" << a[3] << ")" << "=" << endl;
		return (a[0] / (a[1]*1.0)) + (a[2] / (a[3]*1.0));
	case 2:
		cout << "(" << a[0] << "/" << a[0] << ")" << "+" << "(" << a[2] << "/" << a[3] << ")" << "=" << endl;
		return (a[0] / a[0]) + (a[2] / (a[3]*1.0));
	case 3:
		cout << "(" << a[1] << "/" << a[1] << ")" << "+" << "(" << a[0] << "/" << a[3] << ")" << "=" << endl;
		return (a[1] / (a[1]*1.0)) + (a[0] / (a[3]*1.0));
	case 4:
		cout << "(" << a[0] / a[2] << ")" << "-" << a[2] << "/" << a[3] << "=" << endl;
		return a[0] / (a[2]*1.0) + a[2] / (a[3]*1.0);
	default:
		cout << "(" << a[1] << "/" << a[1] << ")" << "+" << "(" << a[0] << "/" << a[3] << ")" <<"="<< endl;
		return (a[1] / (a[1]*1.0)) + (a[0] / (a[3]*1.0));

	}
}
float Multiply()
{
	int range;
	cout << "请输入多少数以内的四则运算：";
	cin >> range;
	cout << endl;
	int a[4] = { 0 };
	srand((unsigned)time(NULL));//	根据系统时间生成随机数
	for (int i = 0; i < 4; i++)
		a[i] = (rand() % range) + 1;
	sort(a, a + 4);	//	将数组进行升序排列
	cout << "请输入答案。(小数精确到后2位！)" << endl;
	switch ((rand() % 9) + 1)
	{
	case 1:
		cout << a[2] << "*" << a[1] << "=";
		return a[2] * a[1];
	case 2:
		cout << a[3] << "*" << a[1] << "*" << a[2] << "=";
		return a[3] * a[1] * a[2];
	case 3:
		cout << a[3] << "*" << a[1] << "=";
		return a[3] * a[1];
	case 4:
		cout << a[4] << "*" << a[1] << "*" << a[2] << "*" << a[3] << "=";
		return a[4] * a[3] * a[2] * a[1];
	case 5:
		cout << a[0] << "*" << "(" << a[1] << "/" << a[3] << ")" << "*" << a[2] << "*" << a[3] << "=";
		return a[0] * (a[1] / (a[3]*1.0)) * a[2] * a[3];
	case 6:
		cout << "(" << a[2] << "/" << a[3] << ")" << "*" << "(" << a[1] << "/" << a[2] << ")" << "*" << a[2] << "=";
		return (a[2] / (a[3]*1.0)) * (a[1] / (a[2]*1.0)) * a[2];
	case 7:
		cout << a[0] << "*" << a[1] << "*" << "(" << a[3] << "/" << a[3] << ")" << "*" << a[3] << "=";
		return a[0] * a[1] * (a[3] / (a[3]*1.0)) * a[3];
	case 8:
		cout << a[2] << "*" << a[1] << "*" << a[2] << "*" << a[3] << "=";
		return a[2] * a[1] * a[2] * a[3];
	case 9:
		cout << a[2] << "*" << "(" << a[1] << "/" << a[3] << ")" << "*" << a[2] << "*" << a[3] << "=";
		return a[2] * (a[1] / (a[3]*1.0)) * a[2] * a[3];
	default:
		cout << a[0] << "*" << a[3] << "*" << a[1] << "=";
		return a[0] * a[3] * a[1];

	}
}
void menu()
{
	cout << "1 加法运算 " << " 2 减法运算 " << " 3 乘法运算 " << " 4 除法运算 " << " 5 混合运算"<<endl;
	cout << "请输入你要做的题目类型：";
}
