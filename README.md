#include <iostream>
#include <stdexcept>
#include <limits>

using namespace std;

class Integer {
private:
    int value;

public:
    Integer(int val = 0) : value(val) {}

    Integer operator+(const Integer& other) {
        long result = static_cast<long>(value) + static_cast<long>(other.value);
        if (result > numeric_limits<int>::max() || result < numeric_limits<int>::min()) {
            throw overflow_error("Addition overflow");
        }
        return Integer(static_cast<int>(result));
    }

    Integer operator-(const Integer& other) {
        long result = static_cast<long>(value) - static_cast<long>(other.value);
        if (result > numeric_limits<int>::max() || result < numeric_limits<int>::min()) {
            throw overflow_error("Subtraction overflow");
        }
        return Integer(static_cast<int>(result));
    }

    Integer operator*(const Integer& other) {
        long result = static_cast<long>(value) * static_cast<long>(other.value);
        if (result > numeric_limits<int>::max() || result < numeric_limits<int>::min()) {
            throw overflow_error("Multiplication overflow");
        }
        return Integer(static_cast<int>(result));
    }

    Integer operator/(const Integer& other) {
        if (other.value == 0) {
            throw runtime_error("Division by zero");
        }
        return Integer(value / other.value);
    }

 
    friend ostream& operator<<(ostream& os, const Integer& obj) {
        os << obj.value;
        return os;
    }


    friend istream& operator>>(istream& is, Integer& obj) {
        int val;
        is >> val;
        obj = Integer(val);
        return is;
    }

    void print() const {
        cout << "Value: " << value << endl;
    }
};

int main() {
    Integer objA(10);
    Integer objB; 

    cout << "Enter a number for objB: ";
    cin >> objB;

    Integer objC;
    try {
        objC = objA + objB;
        cout << "Result of addition: " << objC << endl;

        objC = objA - objB;
        cout << "Result of subtraction: " << objC << endl;

        objC = objA * objB;
        cout << "Result of multiplication: " << objC << endl;

        objC = objA / objB;
        cout << "Result of division: " << objC << endl;

    } catch (const overflow_error& e) {
        cerr << "Overflow error: " << e.what() << endl;
        return EXIT_FAILURE;
    } catch (const runtime_error& e) {
        cerr << "Runtime error: " << e.what() << endl;
        return EXIT_FAILURE;
    }

    return 0;
}
