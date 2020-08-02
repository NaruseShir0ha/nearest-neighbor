# nearest-neighbor
局部最优
#include<iostream>
#include<queue>
#include<stack>
using namespace std;
struct point
{
	float x;
	float y;
};
float dist(point c, point b)
{
	float m;
	m = sqrt(pow((c.x - b.x),2) + pow((c.y - b.y),2));
	return m;
}
int main()
{
	point a[1000],u;
	int i = 0,j,lab,las,d;
	queue<int> V, U,L;//V,U为算法中的处理和未处理的集合，L记录遍历下来确定不是临近点的集合
	stack<int>R;//R记录遍历下来临近点候选集合，其中栈顶为临近元素的标号
	float c=0, m, pr,mid;
	while (cin>>mid)
	{
		//if (mid > 1000)
			//break;
		//a[i].x = mid;
		cin >>a[i].x>>a[i].y;
		V.push(i);
		i++;
	}//输入
	lab = V.front();
	U.push(lab);
	V.pop();
	u = a[lab];//开始处理第一个点
	while (!V.empty())
	{
		pr = 0x7fffffff;//初始化pr
		while (!V.empty())//遍历，寻找和u最邻近的点
		{
			j = V.front();
			m = dist(u, a[j]);
			if (m < pr)
			{
				pr = m;
				R.push(j);
			}
			else
			{
				L.push(j);
			}
			V.pop();
		}
		u = a[R.top()];//R的栈顶是选中的值，将它记录下来
		U.push(R.top());
		R.pop();
		while (!R.empty())
		{
			V.push(R.top());
			R.pop();
		}
		while (!L.empty())
		{
			V.push(L.front());
			L.pop();
		}//上面两个循环是还原V的内容，V少了被选中的
		c += pr;//记下总长度
	}
	while (!U.empty())
	{
		las = U.front();
		cout << las << endl;
		U.pop();
	}
	c += sqrt(pow(a[lab].x - a[las].x, 2) + pow(a[lab].y - a[las].y,2));
	cout << c << endl;
	return 0;
}
