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



#### 图像进阶

#### 对数图

```matlab
>> x = logspace(-1, 1, 100); % logspace(a, b, n) 在 10 的幂 10^a 和 10^b 之间生成 n 个点
>> y = x .^ 2;
>> subplot(2, 2, 1);
>> plot(x, y);
>> title('Plot');
>> subplot(2, 2, 2);
>> semilogx(x, y); % 按照 x 轴的对数刻度绘制
>> title('Semilogx');
>> subplot(2, 2, 3);
>> semilogy(x, y);
>> title('Semilogy'); % 按照 y 轴的对数刻度绘制
>> subplot(2, 2, 4);
>> loglog(x, y);
>> title('Loglog'); % 按照 x 、 y 轴的对数刻度绘制
% 在绘制对数图时应该绘制格线来体现对数图
```



#### plotyy() 绘制双 y 轴图形

```matlab
>> x = 0: 0.1: 20;
>> y1 = 200 * exp(-0.05 * x) .* sin(x);
>> y2 = 0.8 * exp(-0.5 * x) .* sin(10 * x);
>> [AX, H1, H2] = plotyy(x, y1, x, y2); % AX 是原坐标轴， H1 和 H2 是由 y1 和 y2 生成的对象
>> set(get(AX(1), 'Ylabel'), 'String', 'Left Y-axis');
>> set(get(AX(2), 'Ylabel'), 'String', 'Right Y-axis');
>> title('Labeling plotyy');
>> set(H1, 'LineStyle', '--');
>> set(H2, 'LineStyle', ':');
```



#### 直方图

```matlab
>> y = randn(1, 1000);
>> subplot(2, 1, 1);
>> hist(y, 10); % 表示分组为 10
>> title('Bins = 10');
>> subplot(2, 1, 2);
>> hist(y, 50); % 表示分组为 50
>> title('Bins = 50');
% 用于查看整体的趋势
```



#### 条形图

```matlab
>> x = [1 2 5 4 8];
>> y = [x; 1: 5]; % 生成数组 [1 2 5 4 8; 1 2 3 4 5]
>> subplot(1, 3, 1);
>> bar(x);
>> title('A bargraph of vector x');
>> subplot(1, 3, 2);
>> bar(y); % 此时将数组按行分为不同组，按列分为不同 bar
>> title('A bargraph of vector y');
>> subplot(1, 3, 3);
>> bar3(y);
>> title('A 3D bargrapg');
```



#### 条形图的特殊展现形式

```matlab
>> x = [1 2 5 4 8];
>> y = [x; 1: 5];
>> subplot(1, 2, 1);
>> bar(y, 'stacked'); % 将数据堆积起来
>> title('stacked')
>> subplot(1, 2, 2);
>> barh(y); % 在水平方向上生成条形
>> title('Horizontal');
```



#### 饼状图

```matlab
>> a = [10 5 20 30];
>> subplot(1, 3, 1);
>> pie(a);
>> subplot(1, 3, 2);
>> pie(a, [1, 1, 0, 1]); % 矩阵中的 1 表示相邻的块之间是分离的
>> subplot(1, 3, 3);
>> pie3(a, [0, 0, 1, 1]);
```



#### 极坐标图

```matlab
>> x = 1: 100;
>> theta = x / 10;
>> r = log10(x);
>> subplot(1, 4, 1);
>> polar(theta, r);
>> theta = linspace(0, 2*pi);  % linspace(n, m) 返回 n - m 之间 100 个数值
>> r = cos(4 * theta);
>> subplot(1, 4 ,2);
>> polar(theta, r);
>> theta = linspace(0, 2*pi, 6); % linspace(a, b, n) 返回 a - b 之间 n 个数值，相当于将圆分为 5 等份
>> r = ones(1, length(theta));
>> subplot(1, 4, 3);
>> polar(theta, r);
>> theta = linspace(0, 2*pi);
>> r = 1 - sin(theta);
>> subplot(1, 4, 4);
>> polar(theta, r);
```



#### 梯状图及茎状图

```matlab
>> x = linspace(0, 4*pi, 40);
>> y = sin(x);
>> subplot(1, 2, 1);
>> stairs(y);
>> subplot(1, 2, 2);
>> stem(y);
```



#### 练习：绘制图形

```matlab
>> x = linspace(0, 10, 1000);
>> y = sin(pi * x .^ 2 / 4);
>> plot(x, y); % 先在 figure 上绘制线图
>> xx = linspace(0, 10, 51);
>> hold on 
>> g = sin(pi * xx .^ 2 / 4);
>> h = stem(xx, g); % 再绘制茎状图
```



#### 箱型图

```matlab
>> load carsmall
>> boxplot(MPG, Origin)
% 通过 MATLAB 中附带的 carsmall.mat 文件中的数据绘图； MPG 表示示例中年均汽油消耗； Origin 表示国家地区
```



####误差棒图

```matlab
>> x = 0: pi/10: pi;
>> y = sin(x);
>> e = std(y) * ones(size(x)); % 通过标准差得到相应的误差，由于需要与自变量个数一致，故使用 ones 函数
>> errorbar(x, y, e);
```



#### fill 函数

```matlab
>> t = (1: 2: 15)' * pi / 8;
>> x = sin(t);
>> y = cos(t);
>> fill(x, y, 'r'); % fill 函数除了能按照 (x, y) 坐标点进行连线外，还能将包围区域进行填充
>> axis square off % 关闭坐标轴
>> text(0, 0, 'STOP', 'Color', 'w', 'FontSize', 80,...
'FontWeight', 'bold', 'HorizontalAlignment', 'center');
```



#### 练习：绘制 WAIT 图形

```matlab
>> t = (0: 1: 4)' * pi / 2;
>> x = sin(t);
>> y = cos(t);
>> fill(x, y, 'y', 'LineWidth', 2);
>> axis square off
>> text(0, 0, 'WAIT', 'Color', 'k', 'FontSize', 80,...
'FontWeight', 'bold', 'HorizontalAlignment', 'center');
```



#### 练习：更改条形图中竖条颜色

```matlab
>> G = [46 38 29 24 13];
S = [29 27 17 26 8];
B = [29 23 19 32 7];
h = bar(1: 5, [G' S' B']);
>> title('Medal count for top 5 countries in 2012 Olympics');
>> ylabel('Number of medals');
>> xlabel('Country');
>> legend('Gold', 'Sliver', 'Bronze');
>> set(h(1), 'FaceColor', [1 0.9 0.3]);
>> set(h(2), 'FaceColor', [0.5 0.5 0.5]);
>> set(h(3), 'FaceColor', [0.6 0.3 0]);
>> set(gca, 'XTickLabel', {'USA', 'CHN', 'GBR', 'RUS', 'KOR'});
```



#### 通过不同的 z 坐标来反映不同的颜色

```matlab
>> [x, y] = meshgrid(-3: 0.2: 3, -3: 0.2: 3);
>> z = x .^ 2 + x .* y + y .^ 2;
>> surf(x, y, z);
>> box on
>> set(gca, 'FontSize', 16);
>> zlabel('z');
>> xlim([-4 4]);
>> xlabel('x');
>> ylim([-4 4]);
>> ylabel('y')

% -------------------------------------------------------------------------------------------------
>> imagesc(z);
>> axis square
>> xlabel('x');
>> ylabel('y');
% imagesc(A) 将矩阵 A 中的元素值按大小转化为不同颜色，并在坐标轴对应位置处以对应颜色染色
```



#### colormap

```matlab
>> colormap(hot)
>> colormap(jet)
>> colormap(hsv)
>> colormap(cool)
% 剩余部分可上网寻找
```



#### plot3()

```matlab
>> x = 0: 0.1: 3*pi;
>> z1 = sin(x);
>> z2 = sin(2*x);
>> z3 = sin(3*x);
>> y1 = zeros(size(x))
>> y3 = ones(size(x));
>> y2 = y3 ./ 2;
>> plot3(x, y1, z1, 'r', x, y2, z2, 'g', x, y3, z3, 'b');
>> grid on
>> xlabel('x-axis');
>> ylabel('y-axis');
>> zlabel('z-axis');
```



#### meshgrid()

``` matlab
>> x = -2: 1: 2;
>> y = -2: 1: 2;
>> [X, Y] = meshgrid(x, y)

X =

    -2    -1     0     1     2
    -2    -1     0     1     2
    -2    -1     0     1     2
    -2    -1     0     1     2
    -2    -1     0     1     2


Y =

    -2    -2    -2    -2    -2
    -1    -1    -1    -1    -1
     0     0     0     0     0
     1     1     1     1     1
     2     2     2     2     2
% [X, Y] = meshgrid(xgv, ygv);
% meshgrid 生成的 X, Y 是大小相等的矩阵， xgv ， ygv 是两个网格矢量，且同时为行向量
% X：通过将 xgv 复制 length(ygv) - 1 行得到
% Y：首先对 ygv 进行转置得到 ygv' ，将 ygv' 复制 length(xgv) - 1 次
```



#### mesh 与 surf 区别

```matlab
>> x = -3.5: 0.2: 3.5;
>> y = -3.5: 0.2: 3.5;
>> [X, Y] = meshgrid(x, y);
>> Z = X .* exp(-X .^ 2 - Y .^ 2);
>> subplot(1, 2, 1);
>> mesh(X, Y, Z);
>> subplot(1, 2, 2);
>> surf(X, Y, Z);
% 两者区别在于 mesh 命令绘制的图形是一个一排排的彩色曲线组成的网格图，而 surf 命令绘制的是着色的三维曲面
```



#### 使用 contour 函数将图形投影至 x-y 平面

```matlab
>> x = -3.5: 0.2: 3.5;
y = -3.5: 0.2: 3.5;
[X, Y] = meshgrid(x, y);
Z = X .* exp(-X .^ 2 - Y .^ 2);
>> subplot(2, 1, 1);
>> mesh(X, Y,Z);
>> axis square
>> subplot(2, 1, 2);
>> contour(X, Y, Z);
>> axis square
% 此时绘制的 coutour 图形较为稀疏

% -------------------------------------------------------------------------------------------------% contour 函数的其他命令
>> x = -3.5: 0.2: 3.5;
y = -3.5: 0.2: 3.5;
[X, Y] = meshgrid(x, y);
Z = X .* exp(-X .^ 2 - Y .^ 2);
>> subplot(1, 3, 1);
>> contour(Z, [-0.45: 0.05: 0.45]); % 将等高线以规定间隔的线条表示，如此可以增加线条密度
>> axis square
>> subplot(1, 3, 2);
>> [C, h] = contour(Z); % 其中 C 为等高线矩阵，包含定义得到的数据； h 为等高线的句柄；
>> clabel(C, h); % 为图形添加标签：把标签旋转到恰当的角度，再插入到等高线中。只有等高线有足够的空间才能放入，当然这决定于等高线的尺度
>> axis square
>> subplot(1, 3, 3);
>> contourf(Z); % 为图形填充颜色， f 相当于 fill
>> axis square
```



#### 练习： contour 函数综合应用

```matlab
>> x = -3.5: 0.2: 3.5;
y = -3.5: 0.2: 3.5;
[X, Y] = meshgrid(x, y);
Z = X .* exp(-X .^ 2 - Y .^ 2);
>> [C, h] = contourf(Z, [-0.45: 0.05: 0.45]);
>> clabel(C, h);
```



#### meshc 和 surfc 函数

```matlab
% 与 mesh 和 surf 的区别在于，这两个函数还在生产原 mesh 或 surf 图形的同时，还进行了 contour 函数的使用，故直接具有投影图
>> x = -3.5: 0.2: 3.5;
>> y = -3.5: 0.2: 3.5;
>> [X, Y] = meshgrid(x, y);
>> Z = X .* exp(-X .^ 2 - Y .^ 2);
>> subplot(1, 2, 1);
>> meshc(X, Y, Z);
>> subplot(1, 2, 2);
>> surfc(X, Y, Z);
```



#### 角度 (View) 和光线 (Light)

```matlab
>> sphere(50); % 绘制球体
>> shading flat; 
% shading faceted : 默认模式，在曲面或图形对象上叠加黑色的网格线；
% shading flat : 在 shading faceted 的基础上去掉图上的网格线；
% shading interp : 对曲面或图形对象的颜色着色进行色彩的插值处理，使色彩平滑过渡
>> light('Position', [1 3 2]); % 表示灯光照射的位置
>> light('Position', [-3 -1 3]);
>> material shiny; 
% 材质命令
% shiny : 使对象比较明亮，镜反射份额较大，反射光颜色仅取决于光源颜色
% dull : 使对象比较暗淡，漫反射份额比较大，没有镜面亮点，反射光颜色仅取决于光源颜色
% metal : 使对象带金属光泽，镜反射份额很大，背景光和漫反射份额很小，反射光颜色取决于光源和图形表面两者的颜色，该模式为默认设置
% default : 返回默认设置模式
>> axis vis3d off;
>> set(gcf, 'Color', [1 1 1]); 
% 上面的命令表示将背景色设为白色
% [0 0 0] 时为黑色
% 'none' 表示无背景
>> colormap(jet) % 修改 colormap 为 jet
>> view(-45, 20); % 观察点角度

% -------------------------------------------------------------------------------------------------
>> [X, Y, Z] = sphere(64); % 得到球体的相应变量
>> h = surf(X, Y, Z); % 绘制球体
>> axis square vis3d off;
>> reds = zeros(256, 3); % 得到 256 * 3 的 0 矩阵
>> reds(:, 1) = (0:256.-1) / 255;
>> colormap(reds); % 新建 colormap
>> shading interp;
>> lighting phong % 照明模式：使图表面光滑细腻，色彩丰富
>> set(h, 'AmbientStrength', 0.75, 'DiffuseStrength', 0.5);
>> L1 = light('Position', [-1, -1, -1]); % 光照点位置

% 当需要修改光照点位置，而不是增加光照点位置时
>> set(L1, 'Position', [-1, -1, 1]);
```



### GUI

#### 多图绘制

```matlab
% 在 MATLAB 中绘图一般在 axes 上完成，当有多个 axes 时需要指定绘图对象
handles.peaks = peaks(35);
handles.membrane = membrane;
[x, y] = meshgrid(-8: 0.5: 8);
r = sqrt(x .^ 2 + y .^ 2) + eps;
sinc = sin(r) ./ r;
handles.sinc = sinc;
handles.current_data = handles.peaks;
surf(handles.axes1, handles.current_data);

% 或者将最后一行拆开来写
axes(handles.axes1);
surf(handles.current_data);
```



#### 通过移动 Slider 让静态文本显示相应的 Value

```matlab
a = get(handles.slider1, 'Value');
set(handles.text2, 'String', a);
```



#### 存储变量

```matlab
handles.myData = a; % a 可以替换为任意变量
guidata(hObject, handles);
```



#### 使用变量

```matlab
a = handles.myData;
```



#### deploytool

```matlab
% 使用 deploytool 来将代码作为 .exe 文件输出，以便他人运行
% 需要添加 .m 文件和 .fig 文件
```



### 影像分析

#### 读取和显示影像

```matlab
>> I = imread('1.jpg'); % read
>> imshow(I); % show
```



#### 通过像素颜色矩阵修改影像

```matlab
>> for i = 1: size(I, 1)
>> 	for j = 1: size(I, 2)
>> 		if (rem(i, 2) == 0 && rem(j ,2) == 0)
>> 			I(i, j) = 0;
>> 		end
>> 	end
>> end
```



#### 查看影像信息

```matlab
>> imageinfo('1.jpg')
```



#### 通过 imtool 查看影像信息

```matlab
>> imtool('1.jpg')
% 通过该工具内置的 inspect pixel values 查看相应点的像素信息
```



#### 通过 immultiply() 增大像素数值从而使其变亮

```matlab
>> I = imread('rice.png');
>> subplot(1, 2, 1);
>> imshow(I);
>> J = immultiply(I, 1.5); % 表示像素矩阵乘以 1.5 倍
% 可以通过点乘矩阵的方式得到相同的效果 J = 1.5 .* I;
>> subplot(1, 2, 2);
>> imshow(J);
```



#### 通过 imadd 叠加影像

```matlab
>> I = imread('rice.png');
>> J = imread('cameraman.tif');
>> K = imadd(I, J);
>> subplot(1, 3, 1);
>> imshow(I);
>> subplot(1, 3, 2);
>> imshow(K);
>> subplot(1, 3, 3);
>> imshow(J);
% 可以看到叠加后影像变亮了，这是因为相加后相应的像素值变大，但由于最大值为 255 ，所以对于溢出的值都将为 255 ，从而呈现白色
% 对于 imadd 使用的两个图像要保证尺寸相同，即保证其相加的矩阵相同
```



#### 图像直方图

```matlab
>> I = imread('rice.png');
>> imhist(I);
% 对于灰度图，横坐标为灰度，值在 0 - 255 之间，纵坐标表示相应的像素数量
```



#### 使用 histeq 将图像直方图均衡化

```matlab
>> I = imread('pout.tif');
>> I2 = histeq(I);
>> subplot(1, 4, 1);
>> imhist(I);
>> subplot(1, 4, 2);
>> imshow(I);
>> subplot(1, 4, 3);
>> imshow(I2);
>> subplot(1, 4, 4);
>> imhist(I2);
% 简单来说，就是某些图像中有太多亮点或者暗点， histeq 通过一个算法，将亮度重新分配，让人觉得舒服
```



#### 自制 histeq

```matlab
>> H = imread('pout.tif');
>> figure;
>> subplot(1, 2, 1);
>> imshow(H);
>> H = im2double(H); % 将 H 的类型变为 double 类型
>> [M, N] = size(H); % 获取图像的维度
>> [counts, x] = imhist(H); % 读取图像直方图， counts 是每个灰度值的个数， x 表示灰度值
>> location = find(counts ~= 0); % 找到所有像素个数不为 0 的灰度级
>> MinCDF = min(counts(location)); % 找到包含个数最少的灰度级
>> for j = 1: length(location)
    CDF = sum(counts(location(1: j))); % 计算各个灰度级像素个数累计分布
    P = find(H == x(location(j))); % 找到图像中某个灰度级，所有像素点所在位置
    H(P) = (CDF - MinCDF) / (M * N - MinCDF); % 利用灰度换算公式，修改所有位置上的像素值
end
>> subplot(1, 2, 2);
>> imshow(H);
```



### 图像变换

#### 旋转

```matlab
>> I = imread('rice.png'); subplot(1, 2, 1);
>> imshow(I)
>> I = imread('rice.png'); subplot(1, 2, 1);
>> imshow(I)
>> J = imrotate(I, 35, 'bilinear'); % 35 表示旋转角度， bilinear 表示双线性插值
>> subplot(1, 2, 2); imshow(J);
>> size(I)

ans =

   256   256

>> size(J)

ans =

   357   357
% 可以看出图像大小将发生改变
```



#### 存储影像

```matlab
imwrite(I, 'pout2.png');
% 即影像矩阵和文件名
```



#### 利用 threshold 计算米粒数

```matlab
>> I = imread('rice.png');
>> level = graythresh(I) % 通过 graythresh 得到合理的阈值

level =

    0.5137

>> bw = im2bw(I, level); % 根据该阈值，将灰度图转化为黑白图
>> subplot(1, 2, 1);
>> imshow(I);
>> subplot(1, 2, 2);
>> imshow(bw);
```



#### 联系：自制 im2bw

```matlab
>>  I = imread('rice.png');
[M, N] = size(I);
for i = 1: M
       for j = 1: N
           if I(i, j) >= graythresh(I) * 250
               J(i, j) = 1;
           else
               J(i, j) = 0;
           end
       end
end
imshow(J);
```



#### 获得图片背景并在原图中将其减去

```matlab
>> I = imread('rice.png');
>> subplot(1, 3, 1);imshow(I);
>> BG = imopen(I, strel('disk', 15)); % imopen 是一个复杂的函数，中文名为开操作；作用是使对象的轮廓变得光滑，断开狭窄的间断和消除细的突出物； strel 函数用来构件形态学运算中的结构元素，使用语法是 strel(shape, parameters) ；shape 是形状参数，即设置什么样的结构元素； parameters 为控制形状参数大小方向的参数；
% 此处形状参数是 disk ，大小为 15 ，表示创建一个指定半径 15 的平面圆盘形的结构元素
>> subplot(1, 3, 2);imshow(BG);
>> I2 = imsubtract(I, BG); % 通过 imsubtract 将 BG 从 I 中减去
>> subplot(1, 3, 3); imshow(I2);
```



#### 是否减去背景的灰白图对比

```matlab
>> I = imread('rice.png');
>> level = graythresh(I);
>> bw = im2bw(I, level);
>> subplot(1, 2 ,1); imshow(bw);
>> BG = imopen(I, strel('disk', 15));
>> I2 = imsubtract(I, BG);
>> level2 = graythresh(I2);
>> bw2 = im2bw(I2, level2);
>> subplot(1, 2, 2); imshow(bw2);
```



#### 计算米粒数

```matlab
>> I = imread('rice.png');
BG = imopen(I, strel('disk', 15));
I2 = imsubtract(I, BG); level = graythresh(I2);
BW = im2bw(I2, level);
>> [labeled, numObjects] = bwlabel(BW, 8);
% bwlabel 函数将返回一个和 BW 相同大小的矩阵和连通区域的个数。矩阵中包含了 BW 中每个连通区域的类别标签； n 的取值可以为 4 或者 8 ，表示是按照 4 连通寻找区域还是 8 连通寻找，默认为 8 。
```



#### 寻找米粒中的最大值和平均大小

```matlab
>> I = imread('rice.png');
BG = imopen(I, strel('disk', 15));
I2 = imsubtract(I, BG); level = graythresh(I2);
BW = im2bw(I2, level);
[labeled, numObjects] = bwlabel(BW, 8);
>> for i = 1: numObjects
A(i) = length(find(labeled == i));
end
>> max(A)

ans =

   404

>> mean(A)

ans =

  178.5758
```



#### 给米粒表上色彩

```matlab
>> I = imread('rice.png');
BG = imopen(I, strel('disk', 15));
I2 = imsubtract(I, BG); level = graythresh(I2);
BW = im2bw(I2, level);
[labeled, numObjects] = bwlabel(BW, 8);
>> RGB_label = label2rgb(labeled); % 需要使用 label2rgb 函数，将不同标签的米粒标上不同的颜色
>> imshow(RGB_label);
```



#### 米粒数量统计与直方图显示

```matlab
>> I = imread('rice.png');
>> BG = imopen(I, strel('disk', 15)); % 开运算得到背景
>> I2 = imsubtract(I, BG);
>> level = graythresh(I2); % 自动寻找阈值
>> bw = im2bw(I2, level); % 用找到的阈值进行二值化，大于该阈值的灰度将显示为白色
>> [labeled, nums] = bwlabel(bw, 8);
>> for i = 1: nums
A(i) = length(find(labeled == i));
end
>> subplot(1, 4, 1); imshow(I);
>> subplot(1, 4, 2); imshow(I2);
>> subplot(1, 4, 3); imshow(bw);
>> subplot(1, 4, 4); hist(A);
>> j = findobj(gca, 'Type', 'axes');
>> j.XLim = [0, 500];
>> title('米粒数量统计');
>> ylabel('米粒数量');
>> xlabel('米粒尺寸范围');
```



#### 将米粒变为红色

```matlab
>> I = imread('rice.png');
>> BG = imopen(I, strel('disk', 15));
>> I2 = imsubtract(I, BG);
>> level = graythresh(I2);
>> bw = im2bw(I2, level);
>> [sx sy sz] = size(bw); % 获得黑白图的三维度
>> I(:, :, 2) = I(:, :, 1);
>> I(:, :, 3) = I(:, :, 1); % 保证 I 是一个 m * m * 3 的矩阵，从而能够作用 rgb
>> subplot(1, 2, 1);
>> imshow(bw);
>> moto = rgb2ycbcr(I); % 将 rgb 转化为 ycbcr 彩色空间。亮度信息单独由分量 Y 来表示，彩色信息是用两个色差分量 cb 和 cr 来存储；分量 cb 是蓝色分量与参考值的差，分量 cr 是红色分量与参考值的差
>> moto(:, :, 3) = 0; 
>> moto(:, :, 2) = 0; % 由于 moto 中只有红色分量，故将 g 和 b 颜色分量置为 0
>> moto(:, :, 1) = bw(:, :, 1); % 定义红色分量维度大小
>> moto(find(moto(:, :, 1) == 1)) = 255; % 将原图中显示白色的点像素置为 255
>> subplot(1, 2 ,2);
>> imshow(moto);
```



#### 使用 regionprops 查看米粒的特点

```matlab
>> I = imread('rice.png');
BG = imopen(I, strel('disk', 15));
I2 = imsubtract(I, BG);
level = graythresh(I2);
bw = im2bw(I2, level);
>> [labeled, numObjects] = bwlabel(bw, 8);
>> graindata = regionprops(labeled, 'basic'); % 通过 regionprops 将各个区域米粒的 basic 信息存储到 graindata 中
>> graindata(51)

ans = 

  包含以下字段的 struct:

           Area: 155
       Centroid: [112.4258 245.8645]
    BoundingBox: [108.5000 234.5000 8 22]
>> graindata

graindata = 

  包含以下字段的 99×1 struct 数组:

    Area
    Centroid
    BoundingBox
% gradindata 中共有 99 组数据，每组数据都代表一个米粒
```



#### 通过 bwselect 选择米粒显示

```matlab
>> I = imread('rice.png');
BG = imopen(I, strel('disk', 15));
I2 = imsubtract(I, BG);
level = graythresh(I2);
bw = im2bw(I2, level);
>> ObjI = bwselect(bw); % 此时可以通过鼠标进行点选，完成后键入 enter 完成选择
>> imshow(ObjI); % 此时显示的图像将只有选中的几颗米粒
```



### 数值微积分

#### 多项式数值显示

```matlab
>> a = [9, -5, 3, 7];
>> x = -2: 0.01: 5;
>> f = polyval(a, x); % 通过 polyval 函数进行多项式运算
>> plot(x, f, 'LineWidth', 2); % 使用 plot 进行绘制
>> xlabel('x');
>> ylabel('f(x)');
>> set(gca, 'FontSize', 14);
```



#### 多项式微分

```matlab
>> p = [5, 0, -2, 0, 1];
>> polyder(p)

ans =

    20     0    -4     0
% 使用 polyder 函数完成

% -------------------------------------------------------------------------------------------------
% 若希望得到微分后多项式在 x = 7 时的结果
>> polyval(polyder(p), 7)

ans =

        6832
```



#### 练习：在一副上绘制复杂多项式的曲线和其导数的曲线

```matlab
>> x = -2: 0.01: 1;
>> y1 = [20 -7 5 10];
>> y2 = [4 12 -3];
>> f = conv(y1, y2); % conv 用于返回两者的卷积。若两者为多项式系数的向量，对其卷积与将这两个多项式相乘等效
>> g = polyval(f, x);
>> F = polyder(f);
>> g2 = polyval(F, x);
>> plot(x, g, x, g2);
```



#### 多项式积分

```matlab
% 使用 polyint() 完成
>> p = [5 0 -2 0 1];
>> polyint(p, 3)

ans =

    1.0000         0   -0.6667         0    1.0000    3.0000

% 查看积分后多项式在 x = 7 时的值
>> polyval(polyint(p), 7)

ans =

   1.6585e+04
```



#### 求两点之间的斜率

```matlab
% 两点分别为 (1,5) , (2, 7)
>> x = [1 2];
>> y = [5 7];
>> slope = diff(y) ./ diff(x);
>> slope

slope =

     2
% diff() 函数能够返回输入各相邻元素之间的差值
% 示例
>> x = [1 2 5 4 1];
>> diff(x)

ans =

     1     3    -1    -3
```



#### 求微分

根据公式

$$f'(x_{0}) = \lim \limits_{h\to0} \frac{f(x_{0} + h) - f(x_{0})}{h}$$

```matlab
% 对于函数 f(x) = sin(x) ，找到其微分在 x0 = pi/2 且 h = 0.1 时的值
>> x0 = pi / 2;
>> h = 0.1;
>> x = [x0 x0 + h];
>> y = [sin(x0) sin(x0 + h)];
>> m = diff(y) ./ diff(x)

m =

   -0.0500
   
% 当 h 的数值不断缩小时，微分的数值将趋于 0
>> h = logspace(-1, -7, 7); % 从 10^-1 到 10^-7
>> x0 = pi / 2;
>> x = [x0 x0 + h];
y = [sin(x0) sin(x0 + h)];
m = diff(y) ./ diff(x)

m =

   -0.0500   -0.0550   -0.0055   -0.0005   -0.0001   -0.0000   -0.0000
```



#### sin(x) 在区间 0 - 2pi 之间的导数值

```matlab
>> h = 0.5; x = 0: h: 2*pi;
>> y = sin(x);
>> m = diff(y) ./ diff(x);
>> hold on;
>> plot(0: 0.1: 2*pi, sin(0: 0.1: 2*pi));
>> plot(x(1: end - 1), m, '--or'); % end - 1 表示倒数第二个元素，也可以使用 end - n 表示倒数 n + 1 个元素;需要如此操作是因为每次微分都会减少一个数值
>> hold off
>> set(gca, 'XLim', [0, 2*pi]);
>> set(gca, 'YLim', [-1.2, 2]);
>> set(gca, 'FontSize', 25);
>> set(gca, 'XTick', 0: pi/2: 2*pi);
>> set(gca, 'FontName', 'Latex');
>> set(gca, 'XTickLabel', {'0', '\pi/2', '\pi', '3\pi/2', '2\pi'});
>> h = legend('sin(x)', strcat('sin', '''', '(x)')); % strcat 用于水平串联字符串，对于中间 '''' 用于生成 sin'(x) 的 ' ,两侧的表示字符串，中间左侧的表示转义，右侧的才是输出的 ' 
>> set(h, 'FontName', 'Times New Roman');
>> box on
```



#### 不同大小 h 对于微分的影响

```matlab
>> g = colormap(lines);
>> hold on
>> for i = 1: 4
x = 0: power(10, -i): pi;
y = sin(x); m = diff(y) ./ diff(x);
plot(x(1: end - 1), m, 'Color', g(1, :));
end
>> hold off
>> set(gca, 'XLim', [0, pi/2]);
>> set(gca, 'YLim', [0, 1.2]);
>> set(gca, 'FontSize', 18);
>> set(gca, 'FontName', 'Latex');
>> set(gca, 'XTick', 0: pi/4: pi/2);
>> set(gca, 'XTickLabel', {'0', '\pi/4', '\pi/2'});
>> h = legend('h = 0.1', 'h = 0.01', 'h = 0.001', 'h = 0.0001');
>> set(h, 'FontName', 'Times New Roman');
>> box on
% 绘制四种 h 大小对微分曲线的影响图
```



#### 练习：绘制 f(x) 的微分曲线

```matlab
>> hold on
>> for i = 1: 3
x = 0: power(10, -i): 2*pi;
y = exp(-x) .* sin(x .^ 2 / 2);
m = diff(y) ./ diff(x);
plot(x(1: end - 1), m);
end
>> hold off
>> set(gca, 'XLim', [0, 2*pi]);
>> set(gca, 'YLim', [-0.3, 0.3]);
>> set(gca,'FontSize', 18);
>> set(gca, 'FontName', 'Latex');
set(gca, 'XTick', 0: pi/2: 2*pi);
set(gca, 'XTickLabel', {'0', '\pi/2', '\pi', '3\pi/2', '2\pi'});
h = legend('h = 0.1', 'h = 0.01', 'h = 0.001');
set(h, 'FontName', 'Times New Roman');
box on
```



#### 求二次导

```matlab
>> x = -2: 0.005: 2;
>> y = x .^ 3;
>> m = diff(y) ./ diff(x);
>> m2 = diff(m) ./ diff(x(1: end - 1));
>> plot(x, y, x(1: end-1), m, x(1: end-2), m2);
>> xlabel('x', 'FontSize', 18);
>> ylabel('y', 'FontSize', 18);
>> legend('f(x) = x^3', 'f''(x)', 'f''''(x)', 'Location', 'SouthEast');
>> set(gca, 'FontSize', 18);
```



#### 数值积分

有两种方式：矩形规则和梯形规则；矩形规则对应的是中点横坐标规则；梯形规则对应的是中点函数值规则

```matlab
% 通过 sum 函数求解
>> h = 0.05;
>> x = 0: h: 2;
>> midpoint = (x(1: end - 1) + x(2: end)) ./ 2; % 取得各个中点的横坐标
>> y = 4 .* midpoint .^ 3; % 取得对应横坐标的纵坐标
>> s = sum(h .* y) % 求面积并求和

s =

   15.9950
   
% 通过 trapz 函数求解
>> h = 0.05;
>> x = 0: h: 2;
>> y = 4 .* x .^ 3;
>> s = h .* trapz(y); % 求函数值的平均值
>> s

s =

   16.0100
   
% 若将 trapz 自制
>> h = 0.05;
>> x = 0: h: 2;
>> y = 4 .* x .^ 3;
>> trapezoid = (y(1: end-1) + y(2: end)) ./ 2;
>> s = h .* sum(trapezoid)

s =

   16.0100
```



### 函数内嵌套使用函数

在函数内嵌套使用函数不能直接使用函数名，需要使用 @ 作为指针指向需要使用的函数



#### 数值积分

```matlab
>> y = @(x) 1./(x .^ 3 - 2 * x - 5); % 创建函数
>> integral(y, 0, 2) % integral 表示积分， 0 和 2 分别表示下限和上限

ans =

   -0.4605
```



#### 多重积分

```matlab
% 二重积分使用 integral2
>> f = @(x, y) y .* sin(x) + x .* cos(y);
>> integral2(f, pi, 2*pi, 0, pi) % 注意积分上下限需要由内写到外

ans =

   -9.8696

% 三重积分使用 integral3
>> f = @(x, y, z) y .* sin(x) + z .* cos(y);
>> integral3(f, 0, pi, 0, 1, -1, 1)

ans =

    2.0000
```



### 方程式求根

#### 符号变量

```matlab
% 可以通过 syms 和 sym 两种方法定义符号变量
>> syms x
>> x + x + x
 
ans =
 
3*x
 
>> (x + x + x) / 4
 
ans =
 
(3*x)/4

% 两种方式略有不同，但作用相同
>> x = sym('x');
>> x + x + x
 
ans =
 
3*x
 
>> (x + x + x) / 4
 
ans =
 
(3*x)/4
```



#### 通过 solve 与符号变量求解

```matlab
>> syms x
>> y = x * sin(x) - x;
>> solve(y, x) % 此时默认求解的是当 y 为 0 时， x 的数值
 
ans =
 
    0
 pi/2
```



#### 练习：求解方程的根

```matlab
>> syms x
>> y = cos(x) .^ 2 - sin(x) .^ 2;
>> solve(y, x)
 
ans =
 
pi/4

>> syms x
>> y = cos(x) .^ 2 + sin(x) .^ 2;
>> solve(y, x)
 
ans =
 
Empty sym: 0-by-1 % 表示无解析解
```



#### 通过 solve 求解方程组

```matlab
>> syms x y
>> eq1 = x - 2 * y - 5;
>> eq2 = x + y - 6;
>> A = solve(eq1, eq2, x, y)

A = 

  包含以下字段的 struct:

    x: [1×1 sym]
    y: [1×1 sym]

>> A.x
 
ans =
 
17/3
 
>> A.y
 
ans =
 
1/3
```



#### 通过符号表达方程式的解

```matlab
syms x a b
>> solve(a*x^2-b)
 
ans =
 
  b^(1/2)/a^(1/2)
 -b^(1/2)/a^(1/2
```



#### 练习：x 的表达式

```matlab
>> syms x y a b r
>> solve((x - a)^2 + (y - b)^2 - r^2)
 
ans =
 
 a + (b + r - y)^(1/2)*(r - b + y)^(1/2)
 a - (b + r - y)^(1/2)*(r - b + y)^(1/2)
```



#### 练习：求矩阵的逆

```matlab
>> syms a b c d
>> A = [a b; c d];
>> inv(A) % 通过函数 inv 完成
 
ans =
 
[  d/(a*d - b*c), -b/(a*d - b*c)]
[ -c/(a*d - b*c),  a/(a*d - b*c)]
```



#### 使用符号变量求解微分

```matlab
>> syms x
>> y = 4 * x^5;
>> yprime = diff(y)
 
yprime =
 
20*x^4
```



#### 练习：求函数微分

```matlab
% 1
>> syms x
>> f = exp(x^2) / (x^3 - x + 3);
>> diff(f)
 
ans =
 
(2*x*exp(x^2))/(x^3 - x + 3) - (exp(x^2)*(3*x^2 - 1))/(x^3 - x + 3)^2

% 2
syms x y
>> g = (x^2 + x*y - 1) / (y^3 + x + 3);
>> diff(g)
 
ans =
 
(2*x + y)/(y^3 + x + 3) - (x^2 + y*x - 1)/(y^3 + x + 3)^2
```



#### 使用符号变量积分

```matlab
>> syms x
>> y = x^2 * exp(x);
>> z = int(y); % 先对符号进行积分，但是此时有未知常数 k ，需要通过 z(0) = 0 完成 k 的求解
>> z = z - subs(z, x, 0) % subs 函数是将某符号表达式 z 中的 x 值用 第三个参数进行代入
 
z =
 
exp(x)*(x^2 - 2*x + 2) - 2
```



#### 练习：完成函数积分

```matlab
>> syms x
>> f = (x^2 - x + 1) / (x + 3);
>> int(f, 0, 10)
 
ans =
 
log(302875106592253/1594323) + 10
```



#### 通过函数句柄和 fsolve 求解函数

```matlab
>> f2 = @(x) (1.2*x + 0.3 + x*sin(x));
>> fsolve(f2, 0) % 0 是初始猜测值，也可改为其他数值

ans =

   -0.3500
```



#### 使用 fsolve 解二元方程组

```matlab
>> F = @(x) ([2 * x(1)- x(2) - exp(-x(1)); -x(1) + 2 * x(2) - exp(x(2))]);
>> x0 = [-5 -5];
>> fsolve(F, x0)
ans =

    0.3880    0.4865
```



#### fzero 函数求解

```matlab
>> f = @(x) x.^2;
>> fzero(f, 0.1)
ans =

   NaN
% 但对于函数与 x 轴相切时，不能得到解，这与函数内部的算法有关
```



#### 通过选项来精确解

```matlab
>> f = @(x) x.^2;
>> options = optimset('MaxIter', 1e3, 'TolFun', 1e-10); % 前一个选项是最大循环次数，后一个是允许偏差值
>> fsolve(f, 0.1, options)
ans =

   1.9532e-04
```



#### 使用 roots 求多项式的解

```matlab
>> roots([1 -3.5 2.75 2.125 -3.875 1.25])

ans =

   2.0000 + 0.0000i
  -1.0000 + 0.0000i
   1.0000 + 0.5000i
   1.0000 - 0.5000i
   0.5000 + 0.0000i
```



#### 通过 rref 完成高斯消去法

```matlab
>> A = [1 2 1; 2 6 1; 1 1 4];
>> b = [2; 7; 3];
>> R = rref([A b])

R =

     1     0     0    -3
     0     1     0     2
     0     0     1     1
% 此时的 b 便是解
```



#### 逆矩阵

$$A^{-1} =  \begin{bmatrix}  a&b\\ c&d\end{bmatrix} ^{-1} = \frac{1}{det(A)}adj(A)=\frac{1}{det(A)} \begin{bmatrix} d&-b\\-c&a\end{bmatrix}$$

$$det(A) = \begin{vmatrix} ad-bc\end{vmatrix}$$

关于逆矩阵的特性：

$$A = (A^{-1})^{-1}$$

$$(kA)^{-1} = k^{-1} A^{-1}$$



#### 使用克莱姆法则及 inv 完成矩阵求解

$$x = A^{-1}b$$

```matlab
>> A=[1 2 1; 2 6 1; 1 1 4];
>> b = [2; 7; 3];
>> x = inv(A) * b

x =

   -3.0000
    2.0000
    1.0000
    
% 但这种方法当逆矩阵不存在时便无法使用
>> A = [1 2 3 4; 2 4 6 8; 9 8 7 6; 1 3 2 8];
>> inv(A)
警告: 矩阵为奇异工作精度。 

ans =

   Inf   Inf   Inf   Inf
   Inf   Inf   Inf   Inf
   Inf   Inf   Inf   Inf
   Inf   Inf   Inf   Inf
% 因为此时第 2 行为第 1 行的两倍，不满秩
```



#### 通过 cond 查看矩阵是否合适

```matlab
% 当 cond 得出的数值越小，说明矩阵越健康，因为即使矩阵满秩，但如 A 的情况，也会对解产生很大影响
>> A = [1 2 3; 2 4.0001 6; 9 8 7];
>> cond(A)

ans =

   4.3483e+05

>> B = [1 2 3; 2 5 6; 9 8 7];
>> cond(B)

ans =

   45.5623
```



#### 线性系统

用于反应结果 y 与矩阵 A 之间关系的方式

y = Ab

```matlab
% matlab 中通过 eig 函数得到相应的特征向量和特征值
>> [v, d] = eig([2 -12; 1 -5])

v =

    0.9701    0.9487
    0.2425    0.3162


d =

   -1.0000         0
         0   -2.0000
```



###统计

```matlab
>> load stockreturns; % 载入内建数据库
>> x4 = stocks(:, 4);
>> mean(x4)

ans =

  -5.8728e-04

>> median(x4)

ans =

    0.0617

>> mode(x4)

ans =

   -5.8764

>> prctile(x4, 75) % 75% 处的值

ans =

    1.7167

>> max(x4) - min(x4)

ans =

   12.3455

>> var(x4)

ans =

    5.5649

>> std(x4)

ans =

    2.3590
```



#### 绘制频数图

```matlab
>> x = 1: 14;
>> freqy = [1 0 1 0 4 0 1 0 3 1 0 0 1 1];
>> subplot(1, 3, 1);
>> bar(x, freqy);
>> xlim([0 15]);
>> subplot(1, 3, 2);
>> area(x, freqy); % 通过凹凸处的点来表示
>> xlim([0 15]);
>> subplot(1, 3, 3);
>> stem(x, freqy);
>> xlim([0 15]);
```



#### 对于未知频数的数据进行绘图

```matlab
>> x = [1 3 5 5 5 5 7 9 9 9 10 13 14];
>> n = tabulate(x(:)) % tabulate 能够返回数据的频数和频率

n =

    1.0000    1.0000    7.6923
    2.0000         0         0
    3.0000    1.0000    7.6923
    4.0000         0         0
    5.0000    4.0000   30.7692
    6.0000         0         0
    7.0000    1.0000    7.6923
    8.0000         0         0
    9.0000    3.0000   23.0769
   10.0000    1.0000    7.6923
   11.0000         0         0
   12.0000         0         0
   13.0000    1.0000    7.6923
   14.0000    1.0000    7.6923
>> a = n(:, 2)

a =

     1
     0
     1
     0
     4
     0
     1
     0
     3
     1
     0
     0
     1
     1

>> b = a'

b =

     1     0     1     0     4     0     1     0     3     1     0     0     1     1

>> c = 1: 14;
>> subplot(1, 3, 1);
>> bar(c, b);
>> xlim([0 15])
>> subplot(1, 3, 2);
>> area(c, b)
>> xlim([0 15])
>> subplot(1, 3, 3);
>> stem(c, b)
>> xlim([0 15])
```



#### 箱型图

```matlab
>> marks = [80 81 81 84 88 92 94 96 97];
>> boxplot(marks) % 调用即可，并使用线条方框等表示 min 1/4点 1/2点 3/4点 max
>> prctile(marks, [25 75]) % 用来返回相应的分位值

ans =

   81.0000   94.5000
```



#### 练习：通过 boxplot 绘制多组数据箱型图

```matlab
>> load stockreturns;
>> boxplot(stocks)
```



#### 偏态函数与 skewness

```matlab
>> X = randn([10 3]) * 3; % 生成 10*3 的矩阵，并将随机数乘以 3
>> X(X(:, 1) < 0, 1) = 0; % 对于第一列中小于 0 的数，都置为 0
>> X(X(:, 3) > 0, 3) = 0; % 对于第三列中大于 0 的数，都置为 0
>> boxplot(X, {'Right-skewed', 'Symmetric', 'Left-skewed'}); % 绘制 X 的箱型图，并且添加名称
>> y = skewness(X) % 得到三组数据偏度

y =

    0.9526    0.0512   -0.5239

```



#### 峰度

```matlab
>> load stockreturns;
>> x4 = stocks(:, 4);
>> kurtosis(x4)

ans =

    2.8580
% 放映函数是陡峭还是平缓
```



#### 通过 tteset2 进行假设检验

```matlab
% 检验两组数据的平均数是否相同时
>> load stockreturns;
>> x1 = stocks(:, 3);
>> x2 = stocks(:, 10);
>> boxplot([x1, x2], {'3', '10'});
>> [h, p] = ttest2(x1, x2)

h =

     1 % h = 0 时为真， h = 1 时为假


p =

    0.0423 % 一般与 0.05 比较，小于 0.05 说明假设不通过
```



### 回归

```matlab
>> x = [-1.2 -0.5 0.3 0.9 1.8 2.6 3.0 3.5];
>> y = [-15.6 -8.5 2.2 4.5 6.6 8.2 8.9 10.0]; % 输入点的坐标
>> fit = polyfit(x, y, 1) % 通过 ployfit 函数得到合适一次函数的参数值

fit =

    4.9897   -4.4491

>> xfit = [x(1): 0.1: x(end)];
>> yfit = fit(1) * xfit + fit(2);
>> plot(x, y, 'ro', xfit, yfit); % 绘制各个点与回归线
>> set(gca, 'FontSize', 14);
>> legend('Location', 'Northwest', 'data points', 'best-fit'); % 设定图标的位置和名称
```



#### 练习：绘制温度与电压的关系

```matlab
>> T = [20 30 40 50 60];
>> TC = [0.025 0.035 0.05 0.06 0.08];
>> fit = polyfit(T, TC, 1)

fit =

    0.0014   -0.0040

>> x = [T(1): 0.0001: T(end)];
>> y = fit(1) * x + fit(2);
>> plot(T, TC, 'ko', x, y);
```



#### 如何知道 x 和 y 是否具有线性相关性

```matlab
>> x = [-1.2 -0.5 0.3 0.9 1.8 2.6 3.0 3.5];
>> y = [-15.6 -8.5 2.2 4.5 6.6 8.2 8.9 10.0];
>> scatter(x, y); % 绘制散点图
>> box on
>> axis square % 使两坐标轴尺寸相同
>> corrcoef(x, y) % 使用 corrcoef 函数查看相关系数，系数为 -1 <= r <= 1 ,接近 1 时为正相关

ans =

    1.0000    0.9202 % r 为 0.9202 ，可知是正相关，且相关性蛮大的
    0.9202    1.0000
```



#### 查看是否高阶函数符合性更佳

```matlab
>> x = [-1.2 -0.5 0.3 0.9 1.8 2.6 3.0 3.5];
y = [-15.6 -8.5 2.2 4.5 6.6 8.2 8.9 10.0];
figure('Position', [50 50 1500 400]); % 控制图形显示位置、大小
for i = 1: 3
subplot(1, 3, i);
p = polyfit(x, y, i); % 计算各阶函数的系数
xfit = (x(1): 0.1: x(end));
yfit = polyval(p, xfit); % 通过 polyval 获得 yfit
plot(x, y, 'ro', xfit, yfit);
set(gca, 'FontSize', 14);
ylim([-17 11]);
legend('Location', 'SouthEast', 'Data Points', 'Fitted curve');
end
```



#### 练习：尝试 4 5 6 次方程来拟合上述点

```matlab
>> x = [-1.2 -0.5 0.3 0.9 1.8 2.6 3.0 3.5];
y = [-15.6 -8.5 2.2 4.5 6.6 8.2 8.9 10.0];
figure('Position', [50 50 1500 400]);
for i = 4: 6
subplot(1, 3, i-3);
p = polyfit(x, y, i);
xfit = (x(1): 0.1: x(end));
yfit = polyval(p, xfit);
plot(x, y, 'ro', xfit, yfit);
set(gca, 'FontSize', 14);
ylim([-17 11]);
legend('Location', 'SouthEast', 'Data Points', 'Fitted curve');
end
```



#### 多线性回归

```matlab
>> load carsmall; % 载入数据
>> y = MPG;
>> x1 = Weight;
>> x2 = Horsepower;
>> X = [ones(length(x1), 1) x1 x2]; % 由于需要拟合的函数为 y = a + bx1 + cx2 ，所以对于 a 的初始值要定为 1
>> b = regress(y, X); % 求出三个系数 a b c
>> xfit = min(x1): 100: max(x1);
>> x2fit = min(x2): 100: max(x2);
>> [X1FIT, X2FIT] = meshgrid(xfit, x2fit);
>> YFIT = b(1) + b(2) * X1FIT + b(3) * X2FIT;
>> scatter3(x1, x2, y, 'filled'); % 三维散点图
>> hold on
>> mesh(X1FIT, X2FIT, YFIT); % 三维面图
>> hold off
>> xlabel('Weight');
>> ylabel('Horsepower');
>> zlabel('MPG');
>> view(50, 10);
```



#### 对于非线性方程的拟合

使用 cftool



### 内插

#### 线性内插 interp1

```matlab
>> x = linspace(0, 2*pi, 40);
>> x_m = x;
>> x_m([11: 13, 28: 30]) = NaN; % 将部分值设为 Nan ，便不会在图中绘制出来
>> y_m = sin(x_m);
>> plot(x_m, y_m, 'ro', 'MarkerFaceColor', 'r');
>> xlim([0, 2*pi]);
>> ylim([-1.2, 1.2]);
>> box on
>> set(gca, 'FontName', 'Latex', 'FontSize', 16);
>> set(gca, 'XTick', 0: pi/2: 2*pi);
>> set(gca, 'XTickLabel', {'0', '\pi/2', '\pi', '3\pi/2', '2\pi'});
>> 
>> m_i = ~isnan(x_m); % 查看哪几个值是 nan
>> y_i = interp1(x_m(m_i), y_m(m_i), x); % 对 x 中的值都做内插
>> hold on 
>> plot(x, y_i, '-b', 'LineWidth', 2); 
>> hold off
```



#### spline 内插

```matlab
>> x = linspace(0, 2*pi, 40);
>> x_m = x;
>> x_m([11: 13, 28: 30]) = NaN; % 将部分值设为 Nan ，便不会在图中绘制出来
>> y_m = sin(x_m);
>> plot(x_m, y_m, 'ro', 'MarkerFaceColor', 'r');
>> xlim([0, 2*pi]);
>> ylim([-1.2, 1.2]);
>> box on
>> set(gca, 'FontName', 'Latex', 'FontSize', 16);
>> set(gca, 'XTick', 0: pi/2: 2*pi);
>> set(gca, 'XTickLabel', {'0', '\pi/2', '\pi', '3\pi/2', '2\pi'});
>> 
>> hold on 
>> y_i1 = spline(x_m(m_i), y_m(m_i), x);
>> plot(x, y_i1, '-g', 'LineWidth', 2);
>> hold off
>> h = legend('Original', 'Linear', 'Spline');
>> set(h, 'FontName', 'Times New Roman');
% 此时线条相对光滑
```



#### 练习：绘制一组数据点的线性内插线条和 spline 线条

```matlab
>> x = [0 0.25 0.75 1.25 1.5 1.75 1.875 2 2.125 2.25];
>> y = [1.2 1.18 1.1 1 0.92 0.8 0.7 0.55 0.35 0];
>> x_1 = 0: 0.01: 2.25;
>> x_m = x_1;
>> y_1 = interp1(x, y, x_1);
>> plot(x_1, y_1, '-g');
>> hold on 
>> plot(x, y, 'bo');
>> y_m = spline(x, y, x_m);
>> plot(x_m, y_m, 'r');
>> hold off
```



#### spline 与 Hermite 方式比较

```matlab
% 区别在于转折点处
>> x = -3: 3;
>> y = [-1 -1 -1 0 1 1 1];
>> t = -3: 0.01: 3;
>> s = spline(x, y, t);
>> p = pchip(x, y, t);
>> hold on 
>> plot(t, s, ':g', 'LineWidth', 2);
>> plot(t, p, '--b', 'LineWidth', 2);
>> plot(x, y, 'ro', 'MarkerFaceColor', 'r');
>> hold off
>> box on
>> set(gca, 'FontSize', 16);
>> h = legend('Location', 'NorthWest', 'Spline', 'Hermite');
```



#### 平面线性内插

```matlab
>> xx = -2: 0.5: 2;
>> yy = -2: 0.5: 3;
>> [X, Y] = meshgrid(xx, yy);
>> Z = X .* exp(-X.^2 - Y.^2);
>> surf(X, Y, Z); % 画三维图
>> hold on
>> plot3(X, Y, Z+0.01, 'ok', 'MarkerFaceColor', 'r'); % 标红点
>> 
>> xx_i = -2: 0.1: 2;
>> yy_i = -2: 0.1: 3;
>> [X_i, Y_i] = meshgrid(xx_i, yy_i);
>> Z_i = interp2(xx, yy, Z, X_i, Y_i); % 内插
>> surf(X_i, Y_i, Z_i);
>> hold on 
>> plot3(X, Y , Z+0.01, 'ok', 'MarkerFaceColor', 'r'); % 标点
```



#### 平面平滑内插

```matlab
% 在 interp2 中添加参数 'cubic' 即可
>> xx = -2: 0.5: 2;
yy = -2: 0.5: 3;
[X, Y] = meshgrid(xx, yy);
Z = X .* exp(-X.^2 - Y.^2);
surf(X, Y, Z);
hold on
plot3(X, Y, Z+0.01, 'ok', 'MarkerFaceColor', 'r');

xx_i = -2: 0.1: 2;
yy_i = -2: 0.1: 3;
[X_i, Y_i] = meshgrid(xx_i, yy_i);
Z_i = interp2(xx, yy, Z, X_i, Y_i, 'cubic');
surf(X_i, Y_i, Z_i);
hold on 
plot3(X, Y , Z+0.01, 'ok', 'MarkerFaceColor', 'r');
```

