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



