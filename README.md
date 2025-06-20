# C++ Term Project - Perpendicular Bisector
期末project之一，用來找坐標平面上不共線三點形成之三角形的外心，內容如下：

## Rational.h
由於使用浮點數可能丟失精度，於是改用一個`class CRational`存分子`m_numerator`跟分母`m_denominator`。
### Quick reference
- Static Member 
    1. **\_undefined** : 標示為未定義狀態，比如分母為0的情況
- Constructors 
    1. **CRational( int , int )** :  
        傳入分子跟分母來構造CRational，不傳的話分子預設值為0、分母預設值為1
    2. **CRational( const CRational & )** :  
        Copy constructor
    3. **CRational( string )** :  
        可以傳入string如 $\dfrac{a}{b}$ 型(  $a$ 跟 $b$ 皆必須為合法的數字）
- Getter Functions
    1. **getNumerator** :  取得分子
    2. **getDenominator** :  取得分母
- Operations of Fraction
    1. **Add** :  分數相加
    2. **Substract** :  分數相減
    3. **Multiply** :  分數相乘
    4. **Divide** :  分數相除
    5. **Reduction** :  約分
- Operator Overloading 
    - Unary operators
        1. **operator+** : 正號
        2. **operator-** : 負號
    - Binary operators
        1. **operator=** : assign運算子 
        2. **operator>** : 大於
        3. **operator<** : 小於
        4. **operator==** : 等於
        5. **operator!=** : 不等於
        6. **operator+** : 同Add
        7. **operator-** : 同Substract
        8. **operator*** : 同Multiply
        9. **operator/** : 同Divide
        11. **operator>>** :  
            輸入分數，如輸入 `3 2` 表示 $\dfrac{3}{2}$
        12. **operator<<** :  
            輸出分數，如分數 $\dfrac{3}{2}$ 會被輸出成 `3/2`
## Point.h
使用`class CPoint`存放兩個CRational變數`m_x`及`m_y`來表示x座標及y座標。
### Quick reference
- Constructor
    1. **CPoint( CRational , CRational )** :  
        傳入兩個CRational來初始化x座標及y座標，不傳入的話則是會呼叫CRational的default constructor來初始化x座標及y座標
    2. **CPoint( int , int )** :  
        傳入兩個int初始化整數x座標及整數y座標
    3. **CPoint( string , string )** :  
        傳入兩個形如 $(\dfrac{a_x}{b_x},\dfrac{a_y}{b_y})$ 的string，例如傳入`(3/2,1/2)`的話則該點會被初始化成 $(\dfrac{3}{2},\dfrac{1}{2})$
- Getter Functions
    1. **getXCoordinate** : 獲取點的x座標
    2. **getYCoordinate** : 獲取點的y座標
- Operator Overloading
    1. **operator>>** :  
        輸入兩個分數或整數，如：
        - 輸入`3/2 1/2`則會初始化一個點 $(\dfrac{3}{2},\dfrac{1}{2})$
        - 輸入`3 2`則會初始化一個點 $({3},{2})$
    2. **operator<<** :  
        輸出點，如：
        - 點 $(\dfrac{3}{2},\dfrac{1}{2})$ 會以`(3/2,1/2)`的形式被print out
        - 座標是整數的話則會直接輸出整數，例如點 $(3,2)$ 會以`(3,2)`的形式被print out
## Line.h
一個直線方程式可表示成 $ax+by=c$ 的形式。同理，我們使用`class CLine`存放三個CRational變數`coefficient_a`、`coefficient_b`及`const_term`分別指係數 $a$ 、係數 $b$ 以及常數 $c$ 。除此之外，還有使用一個CRational變數`_slope`處理該直線方程式的斜率，以便之後要get其斜率時不需要再做多餘的計算，直接回傳_slope的值即可。  

※ 如果該直線方程式為垂直線，則其斜率不存在。我們使用`CRational::_undefined`來表示該斜率不存在。
### Quick reference
- Constructor
    1. **CLine( CRational a , CRational b , CRational c )** :  
        給定係數 $a$ 、係數 $b$ 以及係數 $c$ 來初始化該直線方程式，即Linear Equation的Standard Form
    2. **CLine( CPoint point , CRational slope )** :  
        給定一點、一斜率來初始化該直線方程式，即Linear Equation的Point-Slope Form
    3. **CLine( CPoint point1 , CPoint point2 )** :  
        給定兩相異點來初始化該直線方程式，即Linear Equation的Two-Point Form
- Getter Functions
    1. **Slope** :  
        獲取該直線方程式的斜率，如斜率不存在，則回傳 `CRational::_undefined`
- Finding Intersection
    1. **Intersect** :  
        傳入一個直線`l2`，回傳該物件與`l2`的交點。如兩直線為平行則throw exception
- Operator Overloading
    1. **operator<<** : 以 $ax+by=c$ 的形式print out
## Circumcenter.cpp
尋找不共線三點所形成三角形之外心
### Functions
1. **PerpendicularBisector** :  
    傳入兩相異點，回傳此兩點之垂直平分線
2. **findCircumcenterPoint** :  
    傳入三個不共線的點，回傳此三點所形成三角形之外心