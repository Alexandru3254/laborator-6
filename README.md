# laborator-6


#include <iostream>
#include <cmath>


class Number {
public:
    
    virtual double media() const = 0;
    virtual ~Number() {} // Destructor virtual
};


class Complex : public Number {
private:
    double real;
    double imag;

public:
    Complex(double r, double i) : real(r), imag(i) {}

    
    double media() const override {
        return (std::abs(real) + std::abs(imag)) / 2.0;
    }
};


class Vector : public Number {
private:
    double elements[10];

public:
    Vector(const double* arr) {
        for (int i = 0; i < 10; ++i) {
            elements[i] = arr[i];
        }
    }

    
    double media() const override {
        double sum = 0.0;
        for (int i = 0; i < 10; ++i) {
            sum += elements[i];
        }
        return sum / 10.0;
    }
};


class Matrix : public Number {
private:
    double matrix[2][2];

public:
    Matrix(const double mat[2][2]) {
        for (int i = 0; i < 2; ++i) {
            for (int j = 0; j < 2; ++j) {
                matrix[i][j] = mat[i][j];
            }
        }
    }

    
    double media() const override {
        return (matrix[0][0] + matrix[0][1] + matrix[1][0] + matrix[1][1]) / 4.0;
    }
};

int main() {
   
    Complex complexObj(1.0, 2.0);
    double vectorArr[10] = {1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0};
    Vector vectorObj(vectorArr);
    double matrixArr[2][2] = {{1.0, 2.0}, {3.0, 4.0}};
    Matrix matrixObj(matrixArr);

    
    Number* numbers[3];
    numbers[0] = &complexObj;
    numbers[1] = &vectorObj;
    numbers[2] = &matrixObj;

    
    for (int i = 0; i < 3; ++i) {
        std::cout << "Media obiectului " << i + 1 << ": " << numbers[i]->media() << std::endl;
    }

    return 0;
}
