# C++
・C++は、C言語にオブジェクト指向を取り入れて拡張した言語
・1998年にC++11(C++0x)、C++14、C++17と3年周期で、言語機能と標準ライブラリが拡張されている。
・モダン言語の良い機能を取り入れている
・C言語で記述したプログラムをほとんどそのまま、C++言語でもコンパイル、実行できるため過去資産の流用や、低レベルのプログラミングにも対応している。
・歴史があるため、同じことをするのに、低レベルから高レベルの記述まで存在する。
・使用するライブラリやコンパイラが対応しているC++のバージョンに合わせて実装する必要がある

# 思うこと
・C言語を拡張しているため、構造体を含む変数に対するイコール(=)はコピーを意味する
・Java、C#、Pythonなどの近代言語では、オブジェクトに対するイコール(=)は参照のみをコピーするが、C++はC言語の互換があるため、オブジェクトの実態をコピーする
・そのため関数で生成したオブジェクトをreturnで受け取る場合にイコールを使用すると、近代言語では参照のみのコピーに対して、C++では実体のコピーとなり、オブジェクトサイズが大きい場合は処理時間がかかり、また一時的にメモリも必要となる。
・その対策として導入されたのが、右辺値(左辺値の概念もこの時生まれた？）、右辺値参照、ムーブ、完全転送の概念と操作方法であり、そのために左辺値と右辺値を共通に扱うためにユニバーサル参照（C++17で転送参照:forwarding referenceという名称に定めた)の手法が誕生した。
・

# C++の絵本 C++が好きになる新しい9つの扉
P11 クラスの中で中身を定義した関数をインライン関数といいます(inline修飾子を使わなくても）
P20 【C++11】クラスを定義するときに、メンバ変数の初期値を設定可能
P41　defineの代わりにconstを使用できる。型を指定できるため、defineよりも厳密に値を定義できる
P41　配列のサイズを定義するときにdefineではなく、constが使える。
  const int BUFSIZE = 10;
  int b[BUFSIZE];  //C言語ではコンパイルエラー
P43　const指定したポインタをconstしていないポインタに代入しようとするとコンパイルエラーになる。代入できてしまうと、代入したポインタから変更できてしまうため
P44　【C++14】2進数リテラル　0b111000001111
P44　文字列リテラル　u8""：UTF-8　u""：UTF-16 U""：UTF-32
P45　【C++11】char16_t：UTF-16文字用の型、char32_t：utf-32文字用の型
P45　【C++11】エスケープ文字を無視する文字リテラル
　　　"C:\\aaa.txt"
    R"C:\aaa.txt"

　　　参考：wchar_tはワイド文字。
P47　【C++11】enum classを使うと、{}内の定義名が、他のenum classの定義名と重複することができるようになった
　　enum class Colors {Red, Green, Yellow}  //
    Colors bookcolor;                       //　C++の場合、「enum」は不要
    bookcolor = Colors::Red;                //　クラス名が必要

P52　ディフォルト引数は最後の引数から順に設定していく必要がある
　　　呼び出し時は、ある引数を省略すると、その引数以降はすべて省略する。
P55　戻り値のみが異なるオーバーロードはできない
P59　書式の設定　
P63　スコープ解決演算子で「::name」はグローバル変数nameを表す
P67　インライン関数はinlineで修飾した関数で、ヘッダファイルに定義する
P77 引数をconst参照にすると、実体渡しのように安全でかつ、大きなデータをポインタ渡しのように高速にデータを渡すことができる
P78　関数に引数は「値渡し」「アドレス渡し」「参照渡し」があるが、値渡しと参照渡しが呼び出し方が同じため、引数の値が関数内で変更されるかわからないという問題がある
　　★関数の中で引数の値を変更する場合は、「アドレス渡し」にするとよいでしょう。
P82　引数がintとポインタでオーバーロードしている場合、NULLを使用すると、ポインタではなくint側の0と認識されるため、期待と異なる関数が呼ばれる場合がある
　　　【C++11】nullptrを使用すると、ポインタと認識されるため、この問題を回避できる
P91　int *p=new int[10]のように確保した配列用メモリは、delete [] p;と書いて開放する。[]が忘れやすいので注意する
P94　コピーコンストラクタ
　　　Person　psn1:
   　 Person　psn2(psn1);　//コピーコンストラクタが呼ばれる

      Person psn3;
      psn3 = psn1;        // operator=()が呼ばれる
P95　クラス定義で、Person(const Person &psn); がコピーコンストラクタ
P95　【c++11】クラス定義で、Person(const Person &psn) = delete;と記述すると、ディフォルトのコピーコンストラクタを使用禁止にできる
P100　クラスA内で、クラスBをfriend宣言すると、クラスBはクラスAのprivateメンバーにアクセスできる
　　　クラス内で、グローバル関数をfriend宣言すると、グローバル関数はクラスのPrivateメンバにアクセスできるようになる
P111　C++は多重継承が可能
    class Fax : public Phone, public Printer {
    };

    ２つの基底クラスのメンバに重複がある場合は、スコープ演算子で解決する
    myFax.Phone::Switch(1);
    myFax.Printer::Switch(1);
P116　基底クラスのメンバ関数を、派生クラスで定義しなおすことを「再定義」するという
P119　基底クラスの仮想関数を派生クラスで再定義することを、オーバーライドと言う
P119　【C++11】仮想関数にfinalをつけると、オーバーライドできなくなる
  virtual void SetPrice(int myprice) final;
P119　【C++11】再定義後の関数に、overrideをつけると、再定義前の関数が仮想関数かどうかをチェックできる
  int GetPrice() override;

P130　静的メンバ変数は、staticをつけて宣言し、cppファイル内で一度だけ初期化する。コンストラクタで初期化しないこと。
P132　静的メンバ関数はクラス宣言で、staticをつけて宣言する

P135　オブジェクトをメンバに持つ場合、コンストラクタの「初期化リスト」で行う。int型(price)なども初期化可能。
    Food::Food() : LimitDate(2005,3,5), price(100) {}

P136　オブジェクトの配列を初期化する
　　Date myDate[ 2] = { Date(2005, 3,5),  Date(2005,4,5) };  // 引数を３つとるコンストラクタが呼ばれる
　　Date myDate[10] = { Date(2005, 3,5),  Date(2005,4,5) };  // 最初の２つは引数を３つとるコンストラクタが呼ばれ、残りは引数無しコンストラクタが呼ばれる
P137　コンストラクタの引数が一つだけの場合、引数の内容だけを記述することもできる
　　DateStr myDateSte1[2] = { DateStr("2005/3/5"), DateStr("2005/4/5") };
　　DateStr myDateSte1[2] = {         "2005/3/5" ,         "2005/4/5"  };  //　上の行と同じ
  
P138　継承する可能性のあるクラスのデストラクタは、仮想関数にする。
　　　派生クラスのポインタを代入した基底クラスポインタをdeleteすると、基底クラスのデストラクタが呼ばれるため、派生クラス専用のリソースが解放されない

P142　テンプレート関数
    template<class T>
    T GetMax(T a, T b){
      T buf;
        :
P144　テンプレートクラス
　　template<class T>
  　class Rectangle{
    public:
     T GetRight(){
       return left + width;
     }
     T left, top, width,height;
    }

Rectangle<int>  rect;
Rectangle<float>  frect;

P144　テンプレート引数が2つ以上ある場合は、複数指定可能
　　template<class T1, class T2>
    class Rectangle2{
       :
P146　標準テンプレートライブラリ　：　STL(Standard Template Library）

P148　反復子：イテレータ
　　イテレータから値にアクセスするときは、＊をつける

    vector<int> v1;
      :
    vector<int>::iterator  itr_first, itr_last, i;
    itr_first = v1.begin();
    itr_last  = v1.end();
    for(i = itr_first; i != itr_last; i++){
      std::cout << *i << std::endl;
    }

P150　【C++11】範囲for　Vector配列を変更しない場合
    vector<int> v1;
    　：
    for(int x : v1){
      std::cout << x << std::endl;    // xはコピーされた値
    }
P151　【C++11】範囲for　Vector配列を変更する場合
    vector<int> v1;
    　：
    for(int &x : v1){  //＆を付与することで参照になる
      x = 50;          // 参照のため、元のvectorの要素を変更する
      std::cout << x << std::endl;    // xは参照
    }

P151　【C++11】範囲forは、範囲が明確はない列でも使用可能
　　int ar[] = { 10, 20, 30 };
    for(int x : ar)
      std::cout << x << std::endl;

P152　【C++11】新しい初期化方法。波括弧でコンストラクタを呼べるようになった。イコールは無し、中括弧を使う
    vector<int>  v1{ 10, 20 };  →　std::initializer_listのコンストラクタを呼ぶ※ため、２つの要素、10,20を登録する
    vector<int>  v1( 10, 20 );  →　(int,int)のコンストラクタを呼ぶため、10個の要素すべてを20で初期化
　
　　※std::vectorが「整数引数2個を受け取るコンストラクタ」と 「std::initializer_listを受け取るコンストラクタ」の両方を持っているが、 
  　　オーバーロード解決時にUniform initialization syntaxはinitializer_listを好むため、波括弧で

P153　【C++11】次のような問題は、波括弧でコンストラクタを呼ぶことで回避可能
　　MikanBox  myMikanBox2();  // コンパイラは、コンストラクタの呼び出しではなく、関数のプロトタイプ宣言と勘違いする
  　myMikanBox2.xxxx();  // コンパイラはmyMikanBox2が関数名だと思っているため、エラーになる

P154　演算子のオーバーロード　st3=st1+st2の場合、st1のoperator+が呼ばれる、引数にst2が入る。returnで返したものをst3に代入
P156　代入演算子のオーバーロード　注意）初期化の場合はコピーコンストラクタが呼ばれる
　　　psn1=psn2の場合、psn1のoperator=が呼ばれる、引数にpsn2が参照渡し
   　Person & operator=(const Person &psn){
       if ( this == &psn ) return *this;  //　自身のオブジェクトを自身に代入しようとした場合は、何もせずそのまま戻す
         :
        (代入処理）
        ：
      　return *this;  //　皿に代入される場合もあるため自信をreturnする（psn3=psn1=psn2)
     }
P158　関数ポインタ　int (*pfn)(int a, int b) = MyFunc;
P160　【C++11】autoキーワード：型推論
    auto a=1000;  //int側に推論
    auto a;      //推論できないのでエラー
P161　【C++11】delctypeキーワード：具体的な型を指定する代わりに、実体と同じ型を使うように指定する。関数ポインタを扱う場合に便利
    int a;
    decltype(a) b;

    int MyFunc(int a, int b);
    decltype(&MyFunc)  pfn = Myfunc;
P162　関数オブジェクト
    class OutputNum{
    public:
      void operator()(int num){  //()演算子をオーバーロードすると関数オブジェクトになる
        cout << 100 + num << endl;  
    }
    vector<int> v1{10, 20, 30};
    OutputNum  out;
    foreach(v1.begin(), v1.end(), out);  // v1のbegin()からend()の範囲で、out関数オブジェクトを呼ぶ
P163　【C++11】ラムダ式を使用すると関数オブジェクトを簡単に作成できる
    auto out2 = [](int num){ cout << 100 + num << endl; };
P168　キャスト演算子
  const_cast<T>(v)      : constを取り除く
  dynamic_cast<T>(v)　  : 基底クラスのポインタ(または参照)を派生クラスのポインタ(または参照)へ変換する
  static_cast<T>(v) 　  : C言語のキャストに近い使い方。ただしconstは取り除けない
　　　　　　　　　　　　　 int*をvoid*にするとか、unsigned char*を構造体のポインタにするなどはこっち。
  reinterpret_cast<T>(v):まったく違う型にキャストできる。例えば関数を違う関数ポインタにキャストするとか、ポインタをint型にするなど
  
# 1週間でC++の基礎が学べる本　亀田健司
・string型　＝は文字列が同じ、大なり小なりは文字数の比較
・bool型　小文字true、false
・メンバ名がm_で始まる命名規則は、ハンガリアン記法もしくはハンガリー記法と呼ばれる
・多重継承は難しいため推奨されない。多言語では禁止されている。インタフェースの多重継承はうまくいく
・コンストラクタは基底クラスのものの後に、派生クラスのものが実行される。デストラクタは逆
・ポリモーフィズム(多相性）は、ある操作（メンバ関数）に対してオブジェクトに合わせた動作、もしくは引数に合わせた動作をすることをいう。
　・オーバーライドはアドホック多相
　・テンプレートはパラメータ多相と呼ばれる
  ・オーバーライドはサブタイピング多相と呼ばれる
・vectorクラスではデータの挿入はできないが、listは可能。同様にvectorにはremove関数が存在しない
　vectorは配列の延長。
・mapクラスは連想配列
　map<string, int>  score;
  score["tom"] = 100;
  score["Bob"] = 80;
・setクラスは集合を扱う。同じデータは１つしか登録できない。
　set<string>  names;
  names.insert("Tom");
  names.insert("Tom");
  names.insert("Tom");
  →Tomは1個しか登録されない
・stackはFILO、queueはFIFO
  stack<int>  stk;
  stk.push(1);
  stk.empty()
    stk.top();  //値取り出し
    stk.pop();  //値削除
    
  queue<int>  que;
  que.push(1);
  que.empty()
    que.front();  //値取り出し
    que.pop();  //値削除

  queue<int>  que;

・クラスの相互参照
  class B;
　class A(){
     B  b;
  }
・const メソッドはインスタンス内の変数を操作できない
  class A{
    int getNum() const;
  }
  int A::getNum() const {  //実装にもconstをつける
  }
・インタフェースとは純粋仮想関数のみで構成されたクラス。JavaやC#のインタフェースに近いもの。
・演算子のオーバーロードの定義は、自身に影響を及ぼす場合はクラス内に定義し、そうではない場合はクラス外で定義する
　代入演算子はクラス内に、代入演算子はクラス外でオーバーロードする。代入演算子は当たらに生成したインスタンスを返すため。
class Vector2D{
public:
  Vector2D& operator=(const Vector2D &v);  // 代入演算子は「自身を書き換えるため」クラス内に定義。自身の参照を変えることが可能
  Vector2D& operator+=(const Vector2D &v);  // ＋＝も同様
  Vector2D& operator-=(const Vector2D &v);  // ー＝も同様
};
//算術演算子は、新たに生成したインスタンスを返却するため、クラス外で定義。returnは値渡し。
Vector2D operator+(const Vector2D &v1, const Vector2D &v2){
  Vector2D  v;
   :
  return v;  //値を返す。値渡しなので呼び元はコピーする
}
Vector2D operator-(const Vector2D &v1, const Vector2D &v2);

# 【C++11】右辺値参照・ムーブセマンティクス
https://cpprefjp.github.io/lang/cpp11/rvalue_ref_and_move_semantics.html

# コンストラクタ
・コンストラクタのエラーを唯一伝える方法が例外のみ


# 関数の入出力について
・関数への入力は、引数で実体渡しもしくはconstの参照渡しにする
・関数から出力は、なるべく実態をreturnで返す
・関数からの出力を引数にする場合はポインタ渡しとする


# 参考
・
・
