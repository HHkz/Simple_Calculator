# AMI_Calculator

��֧���Զ��庯���ļ򵥼��������Ǳ���ԭ��С��ϰ��

# 1 ����

## 1.1 ����

��C++�а���`src/AMI_Calcu.hpp`����

������������ݾ��������ռ�`AmiCal`�¡�

## 1.2 ��Ҫ�ӿ�

|�ӿ�|����|
|:---:|:---:|
|`double etod(const std::string& _expr)`|��`_expr`�еı���ʽ����Ϊ˫����ʵ��|
|`int etoi(const std::string& _expr)`|��`_expr`�еı���ʽ����Ϊ32Ϊ����|

## 1.3 ����ʽ

### 1.3.1 ����

�����ǿɱ����ܵĳ���ֵ���ͣ�

1. ʮ��������������`123`, `114514`
2. `ʮ��������.ʮ��������`������`123.456`, `0.123`
3. `.ʮ��������`������`.123`

### 1.3.2 ���

�����ǿɱ����ܵ���������ͣ�

`+`, `-`, `*`, `/`, `\`, `%`, `(`, `)`, `,`

### 1.3.3 ����

`AMI_Calculator`��������Ϊ����`ID(Para1, Para2, ..)`����ʽ������֧����������

#### 1.3.3.1 Ԥ������

`AMI_Calculator`�ṩ����Ԥ������

|����|�﷨|����|ʾ��|
|:---:|:---:|:---:|:---:|
|`sin`|`sin(double)`|���ز����Ļ���-����ֵ|`sin(3)`|
|`cos`|`cos(double)`|���ز����Ļ���-����ֵ|`cos(2)`|
|`pow`/`power`|`pow(double, double)`|���ص�һ�����ĵڶ���������|`pow(2,2)`|

Ԥ�������ڵ���ʱ��ִ�������飬����������붨�岻ƥ�䣬�᷵��һ��������ߴ���

#### 1.3.3.2 �Զ��庯��

�����ʹ�ýӿ�`insert_function(str, function)`����һ��`std::string`��һ��`double(*)(const vector<double>&)`���������ڰ�֮��`AMI_Calculator`����ʶ������Զ��庯����

���Զ��庯����`std::string`�����к���������ͻ�������һ�θ���Ϊ׼��

�Զ��庯�������Զ�ִ�������飬Ӧ�ں�����������ʵ�֡�

### 1.3.4 ��

`AMI_Calculator`�궨��Ϊ����`$`֮����ַ���������Ԥ�����׶�չ��Ϊ�̶����ַ��������ɺ�˼��㡣

#### 1.3.4.1 Ԥ����

`AMI_Calculator`�ṩ����Ԥ����

|��|չ�����|
|:---:|:---:|
|`e`|`2.718281828`|
|`pi`|`3.14159265`|

#### 1.3.4.2 �Զ����

�����ʹ�ýӿ�`insert_macro(macro, value)`����һ��`std::string`��һ��`std::string`���������ڰ�֮��`AMI_Calculator`����ʶ����ĺꡣ`macro`�еĺ겻��Ҫ��`$`��

���Զ�����`std::string`�����к������ͻ�������һ�θ���Ϊ׼��

## 1.4 ������

`AMI_Calculator`���м򵥵Ĵ�����������

### 1.4.1 ������Ϣ

1. `Ami001 - Lexical error`, �ʷ�����˵����Ĵ��д����Ų����ϴʷ��淶�Ĵʷ���Ԫ���ڷ����˴���֮ʱ��`AMI_Calculator`��ָ�����󴮿�ʼ��λ�úʹʷ���Ԫ�Ĵʷ�ֵ��
2. `Ami002 - Syntax error`, �﷨����˵����Ĵ���Ȼ�ʷ���ȷ�������д����Ų������﷨�淶�Ĵʷ���Ԫ��ϡ��ڷ����˴���֮ʱ��`AMI_Calculator`��ָ������ʷ���Ԫ��ʼ��λ�úʹʷ���Ԫ�Ĵʷ�ֵ��
3. `Ami003 - Math error`, ��������д��󡣺ܴ��������ΪΪһ�����������˴�������Ĳ�����
4. `Ami0031 - Semantic warning`, ���徯�档��Ϊһ�����������˹���Ĳ����������ɾ�������б�ĩβ�ĳ����涨�����Ĳ������������Կ������С�
5. `Ami0032 - Semantic error`, ���������Ϊһ�����������˹��ٵĲ�����
6. `Ami004 - Preprocesser error: undefined marco`, Ԥ����������: δ����ꡣ��������һ��δ����ĺꡣ
7. `Ami005 - Preprocesser error: unclosed macro`, Ԥ����������: �Ǳպϵĺ���š�������������������š�
8. `Ami100 - Inner error`, �������������߲����㡣��������뽫�������д��`issue`�С�

### 1.4.2 ���󷵻�ֵ

һ�����������κδ������м���ӿڵķ���ֵ����ͳһΪ��

|�ӿ�|���󷵻�ֵ|
|:---:|:---:|
|`etod`|`NaN`|
|`etoi`|`0`|

# 2 ʵ��

## 2.1 ����