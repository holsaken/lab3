#include <iostream>
#include <stdexcept>

class Integer {
private:
    int value;

public:

    Integer(int val = 0) : value(val) {}


    Integer operator+(const Integer& other) {
        long result = static_cast<long>(value) + static_cast<long>(other.value);
        if (result > INT32_MAX || result < INT32_MIN) {
            throw std::overflow_error("Addition overflow");
        }
        return Integer(static_cast<int>(result));
    }

    
    Integer operator-(const Integer& other) {
        long result = static_cast<long>(value) - static_cast<long>(other.value);
        if (result > INT32_MAX || result < INT32_MIN) {
            throw std::overflow_error("Subtraction overflow");
        }
        return Integer(static_cast<int>(result));
    }

   
    Integer operator*(const Integer& other) {
        long result = static_cast<long>(value) * static_cast<long>(other.value);
        if (result > INT32_MAX || result < INT32_MIN) {
            throw std::overflow_error("Multiplication overflow");
        }
        return Integer(static_cast<int>(result));
    }

  
    Integer operator/(const Integer& other) {
        if (other.value == 0) {
            throw std::runtime_error("Division by zero");
        }
        return Integer(value / other.value);
    }

   
    void print() const {
        std::cout << "Value: " << value << std::endl;
    }
};

int main() {
    Integer objA(10);
    Integer objB(5); 
    Integer objC;

    try {
        objC = objA + objB;
        objC.print();
        objC = objA - objB;
        objC.print();
        objC = objA * objB;
        objC.print();
        objC = objA / objB;
        objC.print();
    } catch (const std::overflow_error& e) {
        std::cerr << "Overflow error: " << e.what() << std::endl;
        return EXIT_FAILURE;
    } catch (const std::runtime_error& e) {
        std::cerr << "Runtime error: " << e.what() << std::endl;
        return EXIT_FAILURE;
    }

    return 0;
}
