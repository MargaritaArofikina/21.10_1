# 21.10_1

// Реализуйте структуру Rational для работы с рациональными числами, как с несократимыми дробями. В программе должно присутствовать описание структуры и программа, показывающая работоспособность структуры.



#include <iostream>
using namespace std;

int gcd(int a, int b){
	if (b == 0){
		return a;
	}
	return gcd(b, a%b);

}

struct rational {
	int m;
	int n;
	rational(int a, int b){
		m = a / gcd(a, b);
		n = b / gcd(a, b);
	}
	rational(int a){
		m = a;
		n = 1;
	}
	rational(){
		m = 0;
		n = 1;
	}


	rational &operator = (const rational &A){   //присвоение =
		m = A.m;
		n = A.n;
		return *this;
	}
	rational &operator += (const rational &A){    //сложение +=
		m = ((A.m * n) + (m * A.n));
		n *= A.n;
		int d = gcd(m, n);
		m /= d;
		n /= d;
		return *this;
	}
	rational &operator -= (const rational &A){    //вычитание -=
		m = ((A.n * m) - (A.m * n));
		n *= A.n;
		int d = gcd(m, n);
		m /= d;
		n /= d;
		return *this;
	}
	rational &operator *= (const rational &A){    //умножение *=
		m *= A.m;
		n *= A.n;
		int d = gcd(m, n);
		m /= d;
		n /= d;
		return *this;
	}
	rational &operator /= (const rational &A){    //деление /=
		m *= A.n;
		n *= A.m;
		int d = gcd(m, n);
		m /= d;
		n /= d;
		return *this;
	}
};



rational &operator + (rational A, const rational &B) {    // +
	return A += B;
}
rational &operator - (rational A, const rational &B) {    // -
	return A -= B;
}
rational &operator * (rational A, const rational &B) {    // *
	return A *= B;
}
rational &operator / (rational A, const rational &B) {    // /
	return A /= B;
}


bool operator == (const rational &A, const rational &B) {    // ==
	return ((A.m == B.m) && (A.n == B.n));
}
bool operator != (const rational &A, const rational &B) {    // !=
	return ! (A == B);
}
bool operator > (const rational &A, const rational &B) {    // >
	return ((((A.m*B.n) - (B.m * A.n)>0) && (A.n*B.n > 0)) || (((A.m*B.n) - (B.m * A.n) < 0) && (A.n*B.n < 0)));
}
bool operator < (const rational &A, const rational &B) {    // <
	return ((((A.m*B.n) - (B.m * A.n)<0) && (A.n*B.n > 0)) || (((A.m*B.n) - (B.m * A.n) > 0) && (A.n*B.n < 0)));
}
bool operator >= (const rational &A, const rational &B) {    // >=
	return !(A < B);
}
bool operator <= (const rational &A, const rational &B) {    // <=
	return !(A > B);
}


istream &operator >>(istream &in, rational &A)    // >>
{
	in >> A.m >> A.n;
	int d = gcd(A.m, A.n);
	A.m /= d;
	A.n /= d;
	return in;
}
ostream &operator <<(ostream &out, const rational &A)    // <<
{
	out << A.m << "/" << A.n;
	return out;
}





int main() {

	rational l;
	cin >> l.n >> l.m;
	cout << l;


	return 0;
}
