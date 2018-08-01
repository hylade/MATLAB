## MATLAB教程

### 第一章 基础准备及入门

#### 续行输入法P4

MATLAB 中使用 3 个或 3 个以上的连续黑点表示"续行"，即表示下一行是上一行的继续

```matlab
>> S=1-1/2+1/3-1/4 +...
1/5-1/6+1/7-1/8

S =
	0.6345
% 本例中包含"赋值号"，因此表达式的计算结果被赋给了变量 S
% 结果执行后，变量 S 会自动保存在 MATLAB 的 Workplace 工作内存中，以供后用。若用户不用 clear 命令清楚它，或对它重新赋值，那么该变量将会一直保存在工作内存中，直到 MATLAB 命令窗被关闭为止
```



#### 变量名检验P5

```matlab
% 检验 Varname 是否关键词的运行命令（关键词指： for 、 end 等）
>> iskeyword Varname
% 返回值为 1 ，则为关键词，若为 0 ，则非关键词

% 检验 Varname 是否为 MATLAB 自用变量名、函数名、文件夹名等的运行命令（如： pi 、 sin 等）
>> exist Varname
% 若返回值为 0 ，表示不同于 MATLAB 自用变量名、函数名、文件夹名等的运行命令
```



#### 特殊数值的专用变量名P6

```matlab
>> format long e % 对浮点数采用16位数字的科学记述格式：等同于 longE 形式，此时 double 值的小数点后包含 				    15 位数， single 值的小数点后包含 7 位数
>> RMAd=realmax('double') % 双精度类型（默认）时最大实数

RMAd =

    1.797693134862316e+308

>> RMAs=realmax('single') % 单精度类型时的最大实数

RMAs =

  single

   3.4028235e+38

>> IMA64=intmax('int64') % int64整数类型时最大正整数

IMA64 =

  int64

   9223372036854775807
>> IMA32=intmax % int32(默认)整数类型时最大正整数

IMA32 =

  int32

   2147483647

>> IMA16=intmax('int16') % int16 整数类型时最大正整数

IMA16 =

  int16

   32767

>> el=eps % 双精度表达 1 时的绝对精度

el =

     2.220446049250313e-16

>> e2=eps(10) % 双精度表达 10 时的绝对精度

e2 =

     1.776356839400250e-15

>> pi % 圆周率

ans =

     3.141592653589793e+00
```



#### 复数表示方法P8

```matlab
% 经典教科书的直角坐标表示法
>> z1 = 4 + 3i

z1 =

   4.0000 + 3.0000i

% 采用运算符构成的复数直角坐标表示法和极坐标表示法
>> z2=1+2*i

z2 =

   1.0000 + 2.0000i

>> z3=2*exp(i*pi/6)

z3 =

   1.7321 + 1.0000i

>> z=z1*z2/z3

z =

   1.8840 + 5.2631i
   
% 复数的实虚部、模和幅角计算
>> real_z = real(z) % 给出复数 z 的实部

real_z =

    1.8840

>> image_z = imag(z) % 给出复数 z 的虚部

image_z =

    5.2631

>> magnitude = abs(z) % 给出复数 z 的模

magnitude =

    5.5902

>> angle_z_radian = angle(z) % 以弧度为单位给出复数 z 的幅角 arctan（b/a）

angle_z_radian =

    1.2271

>> angle_z_degree = angle(z) * 180 /pi % 度数单位

angle_z_degree =

   70.3048
% 对于同一个表达式的变量名、数字、运算符、虚单元符之间都不要输入空格（尽量）
```



#### MATLAB中复数运算及可视化能力P9

```matlab
% 在一行中输入多条命令
>> z1=4+3i;z2=1+2i; % 但各命令之间要用"分号"或"逗号"分开；当命令后使用"分号"结尾时，使运算结果不显示
% MATLAB的运算符定义再复数域上
>> z12=z1+z2; % 实现复数运算
>> clf % clf 清空图形窗
>> hold on % 使 3 个命令绘制的图形出现在同一张图纸上
>> plot([0,z1,z12],'-b','LineWidth',3) 
>> plot([0,z12],'-r','LineWidth',3)
>> plot([z1,z12],'ob','MarkerSize',8) % 根据各个点坐标连线
>> hold off % 释放"同图纸绘图控制"
>> grid on % 画图纸分格线
>> axis equal % 横轴、纵轴等刻度
>> axis([0,6,0,6]) % 标定刻度大小
>> text(3.5,2.3,'z1') % 在目标位置写文字
>> text(5,4.5,'z2')
>> text(2.5,3.5,'z12')
>> xlabel('real') % 给坐标轴命名
>> ylabel('image')
```





#### MATLAB 方根运算规则及图形表现P10

```matlab
% 对于 MATLAB 中的负数开方计算，对于求幂算符计算，只能得到处于第一象限的方根，若想求得实根，可以通过专门命令 nthroot 求得
>> a=-8 % 给出第一象限的 3 次根

a =

    -8

>> r_a=a^(1/3)

r_a =

   1.0000 + 1.7321i

>> r_n=nthroot(a,3) % 假如实根存在，给出实数根

r_n =

    -2

% 若想获得某个值的全部计算方根，如 -8
% 先构造一个多项式 p(r)=r^3-a
>> p = [1,0,0,-a]; % p 是多项式 p(r)的系数向量；命令末尾的"英文状态分号"使命令运行后，不显示结果；
>> R=roots(p)

R =

  -2.0000 + 0.0000i
   1.0000 + 1.7321i
   1.0000 - 1.7321i
   
>> MR=abs(R(1)); % 计算复根的模， R[1] 表示 R 中第一个解
>> t=0:pi/20:2*pi; % 产生参变量在 0 到 2*pi 之间的一组采样点，间隔为 pi/20
>> x=MR*sin(t);
>> y=MR*cos(t); % 分别计算相应采样点处的 x 和 y 坐标
>> plot(x,y,'b:'),grid on % 绘制一个半径为 R 的圆，并绘制图纸分格线
>> hold on % 开始"同图纸绘图控制"
>> plot(R(2),'.','Markersize',30,'Color','r') % 画第一象限的方根
>> plot(R([1,3]),'o','MarkerSize',15,'Color','b') %  画另两个方根
>> axis([-3,3,-3,3]),axis square % 保证屏幕显示呈真圆
>> hold off
```



#### 数组的一行输入法P11

```matlab
>> AR=[1,3;2,4] % 在此，用逗号分隔"元素"，分号分隔"行"

AR =

     1     3
     2     4
```



#### 数组的多行输入法P11

```matlab
>> AI=[5,7
	  6,8]

AI =

     5     7
     6     8
% 这种输入法为了视觉习惯，同时对于较大的数组也可以考虑使用这种方法
% 在这种输入法中，"回车"用来分隔数组的行
```



#### 复数数组的使用P12

```matlab
% 1) 创建复数数组-1
>> B=[1-5i,3-7i;2-6i,4-8i]

B =

   1.0000 - 5.0000i   3.0000 - 7.0000i
   2.0000 - 6.0000i   4.0000 - 8.0000i
% 创建复数数组-2
AR=[1，3;2，4];AI=[5，7;6，8];
>> A=AR-AI*i

A =

   1.0000 - 5.0000i   3.0000 - 7.0000i
   2.0000 - 6.0000i   4.0000 - 8.0000i
   
% 2) 求复数数组的实部和虚部
>> A_real=real(A)

A_real =

     1     3
     2     4
 >> A_image=imag(A)

A_image =

    -5    -7
    -6    -8

% 3) 求复数数组中各元素的模和幅角——（"标量+循环"法，笨拙！不推荐！）
>> for m=1:2
      for n=1:2
          Am1(m,n)=abs(A(m,n));
          Aa1(m,n)=angle(A(m,n))*180/pi;
      end
end
>> Am1,Aa1

Am1 =

    5.0990    7.6158
    6.3246    8.9443


Aa1 =

  -78.6901  -66.8014
  -71.5651  -63.4349
  
% 4) 求复数数组中个元素的模和幅角——直接法
>> Am2=abs(A)

Am2 =

    5.0990    7.6158
    6.3246    8.9443

>> Aa2=angle(A)*180/pi

Aa2 =

  -78.6901  -66.8014
  -71.5651  -63.4349
% 对于函数 real ， imag ， abs ， angle 同时，并行地作用于数组的每个元素，但对数组作用时间大致与对单个元素的作用所需时间相同，有利于运算速度的提高
```



#### 数组运算能力及MATLAB可视化P14

```matlab
% 画出衰减振荡曲线 y=exp(t/3).*sin(3t) 的图形
>> t=0:pi/50:4*pi; % 定义自变量 t 的取值数组
>> y=exp(-t/3).*sin(3*t); % 计算与自变量相应的 y 数组，注意乘法符前的小黑点
>> plot(t,y,'-b','LineWidth',2) % 绘制曲线
>> axis([0,4*pi,-1,1]) % 定义坐标
>> xlabel('t'),ylabel('y') % 给坐标轴命名

% 命令中 '.*' 符号表示乘法是在两个数组相同位置上的元素间进行的，这种乘法可称为"数组乘"
```



#### 矩阵乘积P14

```matlab
C =

   3.0000 + 2.0000i   2.0000 + 6.0000i
   5.0000 + 3.0000i   4.0000 - 2.0000i

>> D=A*C % 矩阵乘法

D =

  49.0000 -39.0000i  30.0000 -38.0000i
  62.0000 -42.0000i  40.0000 -40.0000i
% 只有当两个矩阵"内维大小相等"时，矩阵乘法才能进行
% 从表达方式看，"矩阵相乘"的命令格式与"标量相乘"命令格式一样，在其他变成语言中，矩阵乘法不得不依赖"循环进行"
```



#### 马尔萨斯人口论（走进数学之数学建模）

认为人口增长是指数型增长



#### 对数

在 MATLAB 中，在为特殊定义时，只能使用 log() （此时等同于 loge() ）， log2() ， log10() 几种默认的对数形式

在需要求特殊的对数时，可以使用换底公式进行变化后求值， log8(7) = loge(7) / loge(8)



#### 矩阵乘法区别

```matlab
% 若适用 "*" 进行乘法运算，则与数学上的乘法相同，即第一行乘以第一列...
% 若使用 ".*" 进行乘法运算，则为相应位置的数相乘

>> A * B

ans =

    13    16
    13    16

>> A .* B

ans =

     3     8
     5    12
```



#### 脚本文件

对于 MATLAB 的脚本文件需要注意命名，若以数字开头，则在运行时将以文件名为代码进行运行，从而易报错，所以对于 MATLAB 的脚本文件，应以字母开头进行命名



#### 输出格式

当使用 fprintf 来输出相应的变量数值时，需要注意数值的格式

当使用 "%f" 时，为定点记数法，当默认时将输出不必要的小数点后 0 值，可以通过在 "%" 后添加 "." 和期望的小数点后位数来进行控制，如 "%.2f" ，此时将输出 2 位小数

也可通过 "%g" 来进行输出，这是一种更加紧凑的 %e 或 %f 形式，将不输出无意义的零



#### MATLAB 条件结构

```matlab
% 示例
num = input('Please enter a number:');
if num > 0
    fprintf('Positive\n');
else
    fprintf('Negative\n');
end
```



#### display 函数

```matlab
>> a = 10;
>> disp(a);
    10
% 若想简单查看某个变量的值，可以使用 disp 函数，且此函数自带 "\n" 效果

>> fr1 = 'apple';
>> fr2 = 'banana';
>> fr3 = 'orange';
>> disp(['apple ', 'banana', 'orange']);
apple bananaorange
>> disp([fr1, fr2, ' ', fr3]);
applebanana orange
% 也可以用来连接变量输出
```



#### 求最大公约数（辗转相除法）

```matlab
a = input('a = ');
b = input('b = ');

r = mod(a, b);
while r ~= 0 % "~=" 表示不等于
    a = b;
    b = r;
    r = mod(a, b);
end
fprintf('%g', b);
```



#### for 循环

```matlab
for i = 1: 5 % 默认为 ++i
    disp(i)
end

for i = 5: -1: -5 % 在端点之间设置步长
    disp(i)
end
```



#### 循环语句中嵌套判断语句

```matlab
s = 0;
for i = 1: 100
    if mod(i, 2) == 1
        s = s + (1 / i);
    else
        s = s - (1 / i);
    end
end
disp(s);
% 注意需要添加两个 "end"
```



#### 利用 for 循环输出各个字符

```matlab
v = [5, 7, 9 10, 13, 3, 2, 1];

for i = v % 注意此处
    disp(i);
end
```



#### 用自行编写的函数实现 100 以内的数值之和

```matlab
function mysum(n)
    s = 0;
    for i = 1: n
        s = s + i;
    end
    fprintf('%g', s);
end
% 此时只将数值之和进行展示，实际不存在返回值

function result = mysum(a, b)
    s = 0;
    for i = a: b
        s = s + i;
    end
    result = s;
end
% 此时，函数将由返回值 result
```



#### 绘制抛物线

```matlab
>> x = -3: 0.01: 3;
>> y = x .* x;
>> plot(x, y, 'blue-o') % 使线条变为蓝色，同时在节点处添加 'o'
>> axis equal % 使两坐标轴的间隔相同
```



#### 绘制直方图

```matlab
>> y = [75 91 105 123.5 131 150 179 203];
>> bar(y)
```



#### 绘制三维螺旋线图

```matlab
>> theta = 0: pi/50: 6*pi;
>> x = cos(theta);
>> y = sin(theta);
>> z = 0:300; % x， y， z 的个数需要相等
>> plot3(x, y, z) % 绘制 3D 图像需要使用 plot3
```



#### 绘制子图

```matlab
x = -4 * pi: pi/6: 4 * pi;
y1 = sin(x);
y2 = sin(2 .* x);
y3 = sin(3 .* x);
y4 = sin(4 .* x);

subplot(2, 2, 1);
plot(x, y1);

subplot(2, 2, 2);
plot(x, y2);

subplot(2, 2, 3);
plot(x, y3);

subplot(2, 2, 4);
plot(x, y4);

% 当第 3 子图的大小为 3 和 4 两子图的大小时
subplot(2, 2, [3, 4]);
```



#### 曲面绘制

```matlab
>> x = -3: 3;
>> y = -3: 3;
>> [X, Y] = meshgrid(x, y); % meshgrid 用于生成网格矩阵
>> Z = X .^ 2 + Y .^ 2;
>> surf(X, Y, Z) % surf 用于绘制面图
```



#### 绘制动态 sin 图

```matlab
x = -2 * pi: 0.1: 2 * pi;
y = sin(x);
h = plot(x, y); % 使 h 中保存线形信息

for i = 1: 100 % 绘制 100 次；若想无限绘制，可以使用 while ture
    x = x + 0.1;
    y = sin(x);
    set(h, 'XData', x, 'YData', y); % set 函数用于将对象重新设定数值
    drawnow; % 实时显示未处理完的图像
end
```



#### 绘制动态弹簧

```matlab
theta = - 10 * pi: 0.1: 10 * pi;
x = cos(theta);
y = sin(theta);
z = theta;
h = plot3(x, y, z);
axis([-1, 1, -1, 1, -40, 40]); % 用于固定坐标轴，防止坐标轴数值发生变化
for i = 1: 100
    z = 0.95 * z; % 不断压缩弹簧
    set(h, 'XData', x, 'YData', y, 'ZData', z); 
    drawnow;
end
for i = 1: 100
    z = z / 0.95; % 不断拉伸弹簧
    set(h, 'XData', x, 'YData', y, 'ZData', z);
    drawnow;
end
% 若想要重复不断的拉伸压缩弹簧，可以在两个循环外加一个 while true 循环
```



#### 绘制时钟

```matlab
t = 0: pi/50: 2 * pi; % 当设置为 0.1 的间隔时，易在圆弧上缺一段，这是因为无法恰好增加至 2 * pi
x = cos(t);
y = sin(t);
hold on;
plot(x, y);
axis equal; % 使坐标间隔相同，圆看上去美观

linex = [0, 1];
liney = [0, 0];
h = plot(linex, liney); % 绘制初始直线

theta = 0;
for i = 1: 1000
    theta = theta + 0.1;
    linex(2) = cos(theta); % 将 linex 中第二个元素进行替换
    liney(2) = sin(theta); % 将 liney 中第二个元素进行替换
    set(h, 'XData', linex, 'YData', liney);
    drawnow;
end
```



------



### MATLAB （台）

#### 如何查看变量

```matlab
% 当在 MATLAB 中输入变量后，可以通过工作区变量名双击查看有关信息
% 或者可以采用如下 who 和 whos 的方式
>> a = 10;
>> who

您的变量为:

a  

>> whos
  Name      Size            Bytes  Class     Attributes

  a         1x1                 8  double        
```



#### 特殊变量

```matlab
1. ans
2. i, j : complex number
3. inf : 1 / 0
4. eps : 2.2204e-016
5. NaN : not a number : inf / inf
6. pi
% 可以通过 iskeyword 查看
```



#### 清除变量

```matlab
% 当使用 clear 时将清除所有变量
% 针对单一变量清除可以使用
clear 变量名
```



#### 变量格式

```matlab
short % 默认格式，保留小数点后 4 位
long % 对于 double 变量，小数点后保留 15 位，对于 single 变量，小数点后保留 7 位
shortE % 在小数点后保留 4 位，并且后面跟上科学计数法
longE % 在 long 类型后添加 科学计数法
bank % 使用美国货币单位计数法，在小数点后保留 2 位
hex % 使用 16 进制
rat % 默认格式都使用小数形式，若使用 format rat 则将变为分数形式
```



#### 矩阵输入

```matlab
% 行向量
>> a = [1 2 3 4]

a =

     1     2     3     4
>> b = [1; 2; 3; 4]

b =

     1
     2
     3
     4
```



#### 矩阵索引

```matlab
% 对于矩阵 A
>> A = [1 21 6; 5 17 9; 31 2 7]

A =

     1    21     6
     5    17     9
    31     2     7
% 当索引只有 1 个数字，或多个数字但没有逗号隔开时，将以列优先，搜索该索引对应的矩阵对象
>> A(8)

ans =

     9

>> A([1 3 5])

ans =

     1    31    17

>> A([1 3; 1 3])

ans =

     1    31
     1    31
% 当为二维矩阵且有两个索引时，前者代表行，后者代表列
>> A(3, 2)

ans =

     2

>> A([1 3], [1 3])

ans =

     1     6
    31     7
% 后者第一个 1 表示第一行，第二个 1 表示第 1 列
```



#### 删除矩阵元素

```matlab
% 对于上述 A 矩阵，首先可以通过索引得到要删除的某一行元素
A（3， ：） % 此命令对应的就是 A 矩阵的第 3 行全部元素
A（3， ：） = [] % 此时就能使 A 的第三行元素被删除
```



#### 增广矩阵

```matlab
>> A = [1 2; 3 4]

A =

     1     2
     3     4

>> B = [9 9; 9 9]

B =

     9     9
     9     9

>> F = [A B]

F =

     1     2     9     9
     3     4     9     9

>> S =[A; B]

S =

     1     2
     3     4
     9     9
     9     9
```



#### 特殊矩阵

```matlab
eye(n) % n 阶单位矩阵
zeros(n1, n2) % n1 * n2 矩阵中元素都为 0
ones(n1, n2) % n1 * n2 矩阵中元素都为 1
diag(n1, n2) % 对角线矩阵，n1 ， n2 为对角线上元素，其余元素都为 0 的矩阵
```



#### 某些矩阵相关函数

```matlab
% max()
A =

     1     2     3
     0     5     6
     7     0     9

>> max(A)

ans =

     7     5     9 % 当使用单个 max 函数，返回各列的最大值

>> max(max(A))

ans =

     9 % 能够返回各列最大值的最大值，即矩阵最大值
     
% min() 函数用法与 max() 函数相同


>> sum(A)

ans =

     8     7    18 % sum() 函数返回各列的和，若需要求整个矩阵的和，可以再套一个 sum
     
>> mean(A)

ans =

    2.6667    2.3333    6.0000 % 求各列的平均值
    
% -------------------------------------------------------------------------------------------------

>> sort(A)

ans =

     0     0     3
     1     2     6
     7     5     9 % 对 A 各列进行从大到小排序
    
>> sortrows(A)

ans =

     0     5     6
     1     2     3
     7     0     9 % 根据各行元素进行排序
     
% size() 能够返回矩阵的各个维度大小
% length() 能够返回矩阵从左往右的长度

>> find(A == 6)

ans =

     8 % find() 函数能够返回矩阵元素位置
```



#### SWITCH-CASE 语句

```matlab
input_num = 5;
switch input_num % switch 用于确定判断量
    case -1
        disp('negative 1');
    case 0
        disp('zero');
    case 1
        diso('positive 1');
    otherwise
        disp('other value');
end
```



#### 函数使用

```matlab
% 对于函数在使用时，可以同时输入多个量
function x = freebody(x0, v0, t)
    x = x0 + v0 .* t + 1/2 * 9.8 * t .* t;
end
>> freebody([0 1], [0 1], [10 20])

ans =

         490        1981
% 此时程序将 (0 0 10) 和 (1 1 20) 作为两组变量输入
```



#### 练习：将华氏度输出为摄氏度

```matlab
function F2C()
    while true
        F = input('Temperature in F :');
        if isempty(F) % F 是否为空
            break;
        end
        C = (F - 32) * 5 / 9;
        disp(C);
    end  
end
```



#### 函数句柄

```matlab
% 函数句柄能够创建匿名函数，并且不用在 .m 文件中进行定义
>> f = @(x) exp(-2 * x);
>> x = 0: 0.1: 2;
>> plot(x, f(x));
% 如上 f 就是一个函数句柄， @ 就是定义句柄的运算符
```



#### 逻辑运算及赋值

```matlab
% 在 MATLAB 中，索引是从 1 开始

str = 'aardvark';
'a' == str
% 上述代码作用是将一个字符串赋值给 str 变量，第二行是查看 str 变量各个位置的 char 是否等于 'a' ，若等于则返回 1 ，若不等于返回 0
ans =

  1×8 logical 数组

   1   1   0   0   0   1   0   0
   

>> str(str == 'a') = 'Z'

str =

    'ZZrdvZrk'
% 该语句则为赋值，将 str 中 'a' 都变为 'Z'
```



#### 练习：将字符串倒转

```matlab
s1 = 'I like the letter E';
s2 = '';
for i = length(s1): -1: 1
    s2 = [s2 s1(i)];
end
disp(s2);
```



#### 结构体相关函数

```matlab
% 显示Field (字段)名
fieldnames()
% 删除结构体某个字段
rmfield()

% 结构体定义
% 在定义结构体时，字段(field 的名字)和值输入参数必须成对出现
```



#### 元胞数组

```matlab
% 用来存储多种不同的信息
% 在元胞数组定义时需要使用 {} ，有两种定义方式
% 1
>> A(1, 1) = {[1 4 3; 0 5 8; 7 2 9]};
>> A(1, 2) = {'Anne Smith'};
>> A(2, 1) = {3 + 7 * i};
>> A(2, 2) = {-pi: pi: pi};
>> A

A =

  2×2 cell 数组

    {3×3 double        }    {'Anne Smith'}
    {[3.0000 + 7.0000i]}    {1×3 double  }
% 2
>> A{1, 1} = [1 4 3; 0 5 8; 7 2 9];
>> A{1, 2} = 'Anne Smith';
>> A{2, 1} = 3 + 7 * i;
>> A{2, 2} = -pi: pi: pi;
```



#### 元胞数组内容查看

```matlab
% 由于元宝数组中各个元胞可视为指针，指向不同的内容，故元胞数组可以存储不同类型的内容
% 对于上述元胞数组中第 1 个或第 4 个元胞，如何查看内容
A（1， 1） % 只能说明指向的内容是什么
A{1， 1} % 能得到真实的内容
>> A(1, 1)

ans =

  1×1 cell 数组

    {3×3 double}

>> A{1, 1}

ans =

     1     4     3
     0     5     8
     7     2     9
```



#### 矩阵与元胞数组的转换

```matlab
>> a = magic(3) % 用于生成 n 阶魔方矩阵，特点为行、列、对角线元素之和相等

a =

     8     1     6
     3     5     7
     4     9     2

>> b = num2cell(a) % 将 a 转换为元胞数组 b

b =

  3×3 cell 数组

    {[8]}    {[1]}    {[6]}
    {[3]}    {[5]}    {[7]}
    {[4]}    {[9]}    {[2]}
    
% 若想在转换过程中进行分块，将需要的几块放在一起，可以使用 mat2cell()
>> c = mat2cell(a, [1 1 1], 3) % a 表示转换的对象，[1 1 1] ，表示行应该如何划分，这里分为 3 行， 3 表示列不进行划分；注意，行列划分时，其和需要等于矩阵行、列数值

c =

  3×1 cell 数组

    {1×3 double}
    {1×3 double}
    {1×3 double}
>> c{1}

ans =

     8     1     6
```



#### 三维数组

```matlab
>> A{1, 1, 1} = [1 2; 4 5];
>> A{1, 2, 1} = 'Name';
>> A{2, 1, 1} = 2 - 4 * i;
>> A{2, 2, 1} = 7;
>> A{1, 1, 2} = 'Name2';
>> A{1, 2, 2} = 3;
>> A{2, 1, 2} = 0: 1: 3;
>> A{2, 2, 2} = [4 5];
>> A

  2×2×2 cell 数组

A(:,:,1) = 

    {2×2 double        }    {'Name'}
    {[2.0000 - 4.0000i]}    {[   7]}


A(:,:,2) = 

    {'Name2'   }    {[       3]}
    {1×4 double}    {1×2 double}
```



#### 利用 cat 函数拼接数组

```matlab
% 在拼接前需要保证拼接的数组相应的维度是一样的
>> A = [1 2; 3 4];
>> B = [5 6; 7 8];
>> C = cat(1, A, B) % 第一个参数为 1 ，说明需要竖向拼接

C =

     1     2
     3     4
     5     6
     7     8

>> cat(2, A, B) % 第一个参数为 2 ，说明需要横向拼接

ans =

     1     2     5     6
     3     4     7     8

>> cat(3, A, B) % 第一个参数为 3 ，说明需要三维拼接

ans(:,:,1) =

     1     2
     3     4


ans(:,:,2) =

     5     6
     7     8
```



#### 利用 reshape 函数改变数组行列

```matlab
>> A = {'James Bond', [1 2; 3 4; 5 6]; pi, magic(5)};
>> C = reshape(A, 1 ,4)

C =

  1×4 cell 数组

    {'James Bond'}    {[3.1416]}    {3×2 double}    {5×5 double}
% 需要保证前后行、列之积保证相同
```



#### 存储数据

```matlab
% 当使用 MATLAB 时需要保存数据时，可以使用 save 来保存，但会将所有工作区的数据都进行保存
>> a = magic(4);
>> save mydata1.mat % 这种方式当使用记事本打开时，会发现乱码，原因在于 MATLAB 在保存时进行了压缩
>> save mydata2.mat -ascii % 这种方式可以正常打开浏览

% 若需要只保存单一变量时，可以在尾端添加该变量名
>> save mydata3.mat A
```



#### 提取数据

```matlab
% 可以使用 load 进行数据的调用
% 例如对上述保存的数据进行提取
>> load('mydata1.mat')
>> load('mydata2.mat', '-ascii') % 注意利用 ascii 码保存的文件打开方式比较特殊
```



#### 提取 .xlsx 文件数据

```matlab
>> Score = xlsread('04Score.xlsx') % 未定义数值区域，但仍只可以读取数值

Score =

    94    83    89
    76    88    82
    68    72    75

>> Score1 = xlsread('04Score.xlsx', 'B2: D4') % 指定数值区域

Score1 =

    94    83    89
    76    88    82
    68    72    75
% 若需要将其余字符串信息也读取进来可以使用两个返回值
>> [Score Header] = xlsread('04Score.xlsx')

Score =

   94.0000   83.0000   89.0000
   76.0000   88.0000   82.0000
   68.0000   72.0000   75.0000


Header =

  4×4 cell 数组

  1 至 6 列

    {0×0 char}    {'Test1' }    {'Test2' }    {'Test3' }
    {'John'  }    {0×0 char}    {0×0 char}    {0×0 char}
    {'Selina'}    {0×0 char}    {0×0 char}    {0×0 char}
    {'Peter' }    {0×0 char}    {0×0 char}    {0×0 char}
```



#### 利用 xlswrite 对 .xlsx 文件进行改动

```matlab
% 例如对上述 04Score.xlsx 文件求平均值
>> M = mean(Score')'

M =

   88.6667
   82.0000
   71.6667
% 首先先求得平均值，由于文件中求平均值的对象是横向布置的，而 mean 函数只能对竖向对象求平均值，所以需要利用 ' 进行转置，同时为了保存，还要将其结果转置回去，所以共使用了两次转置

>> xlswrite('04Score.xlsx', M, 1, 'E2: E4'); % 第一个参数是文件名；第二个参数是需要添加的对象；第三个参数是 sheet 的序号；第四个变量是该 sheet 中相应的位置
>> xlswrite('04Score.xlsx', {'Mean'}, 1, 'E1'); % 为表格相应的位置添加标题，注意添加标题时变量的格式
```



#### I\O

```matlab
>> x = 0: pi/10: pi; y = sin(x); fid =fopen('sinx.txt', 'w'); % 第一个参数是文件名，第二个参数是允许操作的指令，如 'r' , 'w' , 'w+' 等等； fid 如同指针，将会依次指向文件中各个数值
>> for i = 1: 11
      fprintf(fid, '%5.3f %8.4f\n', x(i), y(i)); % 此处前者数据类型的含义是：共有 5 个数字，小数点后 3 位；后者含义是：共有 8 个数字，小数点后 4 位
   end
>> fclose(fid); % 需要注意每次 open 一个对象，都需要 close 它
>> type sinx.txt

0.000   0.0000
0.314   0.3090
0.628   0.5878
0.942   0.8090
1.257   0.9511
1.571   1.0000
1.885   0.9511
2.199   0.8090
2.513   0.5878
2.827   0.3090
3.142   0.0000

% 读取文件中数据
>>fid = fopen('asciiData.txt', 'r');
i = 1;
while ~feof(fid) % feof 用于检查是否处于文章尾端，若是返回 1 ，若否，返回 0
	name(i, :) = fscanf(fid, '%5c', 1); % 第三个参数是指读取出来的维度大小 sizeA 中
	year(i) = fscanf(fid, '%d', 1);
	no1(i) = fscanf(fid, '%d', 1);
	no2(i) = fscanf(fid, '%d', 1);
	no3(i) = fscanf(fid, '%g', 1);
	no4(i) = fscanf(fid, '%g\n');
	i = i + 1;
end
fclose(fid);
```



### 基础绘图

#### plot + legend

```matlab
>> x = 0: 0.5: 4*pi;
>> y = sin(x);
>> h = cos(x); 
>> w = 1 ./ (1 + exp(-x));
>> g = (1 / (2 * pi * 2) ^ 0.5) .* exp((-1 .* (x - 2 * pi) .^ 2) ./ (2 * 2 ^ 2));
>> plot(x, y, 'bd-', x, h, 'gp:', x, w, 'ro-', x, g, 'c^-');
>> legend('sin(x)', 'cos(x)', 'Sigmoid', 'Gauss function');
% legend 能够为图像添加图例
```



#### 添加标题

```matlab
>> x = 0: 0.1: 2*pi;
>> y1 = sin(x);
>> y2 = exp(-x);
>> plot(x, y1, '--*', x, y2, ':o');
>> xlabel('t = 0 to 2 \pi');
>> ylabel('values of sin(t) and e^{-x}');
>> title('Function Plots of sin(t) and e^{-x}');
>> legend('sin(t)', 'e^{-x}');
% 标题中的特殊字符可以使用 Tex 语言生成
```



#### LaTex 语言及添加箭头

```matlab
>> x = linspace(0, 3);
>> y = x .^ 2 .* sin(x);
>> plot(x, y);
>> line([2, 2], [0, 2 ^ 2 * sin(2)]); % 画竖线
>> str = '$$ \int_{0}^{2} x^2 \sin(x) dx $$'; % 用于在图上输出说明文字
>> annotation('arrow', 'X', [0.32, 0.5], 'Y', [0.6, 0.4]); % arrow 表示箭线，前一个数组表示 x 轴坐标，后一个数组表示 y 轴坐标，但是这里的数字都表示相对值，只能取 [0, 1] 之间的数值
>> text(0.25, 2.5, str, 'Interpreter', 'latex'); % 前两个分别表示 x 轴坐标和 y 轴坐标，为绝对值； str 表示要添加的文字，后两者为固定格式，说明编译器为 latex
```



#### 练习：绘制函数并更改图例位置

```matlab
>> t = 1: 0.1: 2;
>> f = t .* t;
>> g = sin(2 * pi .* t);
>> plot(t, f, 'k.-', t, g, 'ro-');
>> t = 1: 0.01: 2;
>> f = t .* t;
>> g = sin(2 * pi .* t);
>> plot(t, f, 'k.-', t, g, 'ro-');
>> title('Mini Assignment #1');
>> ylabel('f(t)');
>> xlabel('Time(ms)');
>> legend('t^{2}', 'sin(2 \pi t)', 'location', 'NorthWest'); % 将原本处于右上角的图例更改到左上角
```



#### 通过 get 得到函数信息

```matlab
>> x = linspace(0, 2*pi, 1000);
>> y = sin(x);
>> plot(x, y);
>> h = plot(x, y);
>> get(h)
    AlignVertexCenters: 'off'
            Annotation: [1×1 matlab.graphics.eventdata.Annotation]
          BeingDeleted: 'off'
            BusyAction: 'queue'
         ButtonDownFcn: ''
              Children: [0×0 GraphicsPlaceholder]
              Clipping: 'on'
                 Color: [0 0.4470 0.7410]
             CreateFcn: ''
             DeleteFcn: ''
           DisplayName: ''
      HandleVisibility: 'on'
               HitTest: 'on'
         Interruptible: 'on'
              LineJoin: 'round'
             LineStyle: '-'
             LineWidth: 0.5000
                Marker: 'none'
       MarkerEdgeColor: 'auto'
       MarkerFaceColor: 'none'
         MarkerIndices: [1×1000 uint64]
            MarkerSize: 6
                Parent: [1×1 Axes]
         PickableParts: 'visible'
              Selected: 'off'
    SelectionHighlight: 'on'
                   Tag: ''
                  Type: 'line'
         UIContextMenu: [0×0 GraphicsPlaceholder]
              UserData: []
               Visible: 'on'
                 XData: [1×1000 double]
             XDataMode: 'manual'
           XDataSource: ''
                 YData: [1×1000 double]
           YDataSource: ''
                 ZData: [1×0 double]
           ZDataSource: ''
           
% 通过 get(gca) 也可以获得坐标轴的一些参数
```



#### 通过 set 改变参数

```matlab
>> set(gca, 'XLim', [0, 2 * pi]);
>> set(gca, 'YLim', [-1.2, 1.2]);
% 改变上图中坐标轴的范围

>> set(gca, 'FontSize', 25);
% 改变上图中坐标的字符大小

>> set(gca, 'XTick', 0: pi/2: 2*pi);
>> set(gca, 'XTickLabel', 0: 90: 360);
% 改变坐标轴的刻度，改变 XTick 表示相隔多远画刻度线，下一行命令为将上述刻度线添加数值

% 为了使坐标轴上刻度数值显示为符号形式，原 symbol 方式已经被淘汰
>> set(gca, 'FontName', 'LaTeX');
>> set(gca, 'XTickLabel', {'0', '\pi/2', '\pi', '3\pi/2', '2\pi'});

% 改变上述线条 h 的参数
>> set(h, 'LineStyle', '-.',...
'LineWidth', 7.0, 'Color', 'g');
```



#### 删除线条

```matlab
>> delete(h); % 此时线条将被删除
```



#### Marker 参数改变

```matlab
>> x = rand(20, 1); % 生成 20 行 1 列的数值在 [0, 1] 的随机矩阵
>> set(gca, 'FontSize', 18); % 改变字体大小为 18
>> plot(x, '-md', 'LineWidth', 2, 'MarkerEdgeColor', 'k',...
'MarkerFaceColor', 'g', 'MarkerSize', 10); % 生成 x 的图像，-md 表示实线洋红钻石型线条
>> xlim([1, 20]); % 限制 x 坐标轴的范围
```



#### 练习：将前述练习的参数进行修改

```matlab
>> t = linspace(1, 2);
>> f = t .^ 2;
>> h = sin(2 * pi .* t);
>> plot(t, f, 'k-', 'LineWidth', 2);
>> hold on
>> plot(t, h, 'ro', 'MarkerEdgeColor', 'm', 'MarkerFaceColor','k');
>> hold off
>> xlabel('Time(ms)');
>> ylabel('f(t)');
>> title('Mini Assignment #1');
>> legend('t^2', 'sin(2\pit)', 'location', 'NorthWest');
>> set(gca, 'FontSize', 20);
```



#### 多个图像显示

```matlab
>> x = -10: 0.1: 10;
>> y1 = x .^ 2 - 8;
>> y2 = exp(x);
>> figure, plot(x, y1);
>> figure, plot(x, y2);
% figure 能够创建一个用来显示图形输出的对象窗口，所以此处将出现两个图像窗口
% 对于figure，能够通过修改其 Position 属性来改变图像大小及输出位置
>> figure('Position', [left, bottom, width, height]);

% 示例
>> figure('Position', [600, 300, 200, 400]);
>> figure('Position', [600, 300, 200, 400]), plot(x, y1); % 也可以配合 plot 直接生成
```



#### 单个 figure 内生成多个图形

```matlab
>> x = 0: 0.1: 2*pi;
>> t = 0: 0.1: 2*pi;
>> x = 3 * cos(t);
>> y = sin(t);
>> subplot(2, 2, 1); plot(x, y); axis normal
>> subplot(2, 2, 2); plot(x, y); axis square
>> subplot(2, 2, 3); plot(x, y); axis equal
>> subplot(2, 2, 4); plot(x, y); axis equal tight
% 生成四幅图像，但是每幅图像的坐标轴不同
```



#### 图像坐标轴、格线

```matlab
% 是否显示坐标轴
>> axis off 
>> axis on
% 是否显示上侧和右侧的线条
>> box off 
>> box on
% 是否显示格线
>> grid on
>> grid off
```



#### 存储图像

```matlab
% 使用如下命令进行
saveas(gcf, '<filename>', 'formattype');
% 对于 format 有两种，一种是位图，如 png 、 bmp 等；另一种是矢量图，类似 pdf 、 eps 等，建议使用矢量图方法，但是当分辨率高于一定值时，无法使用 saveas 保存矢量图，此时需要使用 print
```

