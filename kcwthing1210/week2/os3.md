# πνλ‘μΈμ€ λκΈ°ν
## π λκΈ° VS λΉλκΈ°
### β λκΈ°
- λ©μλλ₯Ό μ€νμν΄κ³Ό λμμ λ°ν κ°μ΄ κΈ°λλλ κ²½μ°
- μμ²­μ νλ©΄ μκ°μ΄ μΌλ§κ° κ±Έλ¦¬λμ§ μμ²­ν μλ¦¬μμ κ²°κ³Όκ° μ£Όμ΄μ ΈμΌ νλ€.
- μμ²­κ³Ό κ²°κ³Όκ° ν μλ¦¬μμ λμμ μΌμ΄λ¨
- AλΈλμ BλΈλ μ¬μ΄μ μμ μ²λ¦¬ λ¨μ(transaction)λ₯Ό λμμ λ§μΆ€
- ex) ν΄μΌν  μΌ(task)κ° λΉ¨λ, μ€κ±°μ§, μ²­μ μΈ κ°μ§κ° μλ€κ³  κ°μ  νμ λ, λκΈ°μ μΌλ‘ μ²λ¦¬νλ€λ©΄ λΉ¨λλ₯Ό νκ³  μ€κ±°μ§λ₯Ό νκ³  μ²­μ

### β λΉλκΈ°
- μμ²­κ³Ό κ²°κ³Όκ° λμμ μΌμ΄λμ§ μμλ λ¨.
- μμ²­ν κ·Έ μλ¦¬μμ κ²°κ³Όκ° μ£Όμ΄μ§μ§ μμ
- λΈλ μ¬μ΄μ μμ μ²λ¦¬ λ¨μλ₯Ό λμμ λ§μΆμ§ μμλ λ¨
- ex) λΉλκΈ°μ μΌλ‘ μΌμ μ²λ¦¬νλ€λ©΄ λΉ¨λ, μ€κ±°μ§, μ²­μλ κ°κ° λν μμ²΄μ λ§‘κΈ΄λ€. μ μ€ μ΄λ€ κ²μ΄ λ¨Όμ  μλ£λ μ§λ μ μ μλ€. μΌμ λͺ¨λ λ§μΉ μμ²΄λ λμκ² μλ €μ£ΌκΈ°λ‘ νμΌλ λλ λ€λ₯Έ μμμ ν  μ μλ€. μ΄ λλ λ°±κ·ΈλΌμ΄λ μ€λ λμμ ν΄λΉ μμμ μ²λ¦¬νλ κ²½μ°μ λΉλκΈ°λ₯Ό μλ―Έ



# νλ‘μΈμ€ λκΈ°ν
- νλ‘μΈμ€ λκΈ°νλ μ¬λ¬ νλ‘μΈμ€κ° κ³΅μ νλ μμμ μΌκ΄μ±μ μ μ§νλ κ²μ΄λ€. κ°λ Ή μ¬λ¬ νλ‘μΈμ€κ° λμμ νλμ κ³΅μ λ μμμ μ κ·Όνλ €κ³  ν  λ μ΄ νλ‘μΈμ€λ€μ μμλ₯Ό μ νμ¬ λ°μ΄ν°μ μΌκ΄μ±μ μ μ§μμΌμ£Όμ΄μΌ νλ€.

- ex)
``` java
// Test.java
class Test {
	public static void main(String[] args) throws InterruptedException {
		BankAccount b = new BankAccount();
		Parent p = new Parent(b);
		Child c = new Child(b);
		p.start();   // start(): μ°λ λλ₯Ό μ€ννλ λ©μλ
		c.start();
		p.join();    // join(): μ°λ λκ° λλκΈ°λ₯Ό κΈ°λ€λ¦¬λ λ©μλ
		c.join();
		System.out.println("balance = " + b.getBalance());
	}
}

// κ³μ’
class BankAccount {
	int balance;
	void deposit(int amount) {
		balance = balance + amount;
	}
	void withdraw(int amount) {
		balance = balance - amount;
	}
	int getBalance() {
		return balance;
	}
}

// μκΈ νλ‘μΈμ€
class Parent extends Thread {
	BankAccount b;
	Parent(BankAccount b) {
		this.b = b;
	}
	public void run() {   // run(): μ°λ λκ° μ€μ λ‘ λμνλ λΆλΆ(μΉν)
		for (int i = 0; i < 100; i++)
		  b.deposit(1000);
	}
}

// μΆκΈ νλ‘μΈμ€
class Child extends Thread {
	BankAccount b;
	Child(BankAccount b) {
		this.b = b;
	}
	public void run() {
		for (int i = 0; i < 100; i++)
		  b.withdraw(1000);
	}
}
```
- μ¬λ¬ μ°λ λκ° νλμ κ³΅μ  μμμ μ¬μ©νμ¬ λκΈ°ν λ¬Έμ λ₯Ό ν΄κ²°νμ§ λͺ»νμκΈ° λλ¬Έμ μνλ κ° μλμ¬ μ μμ
- κ³΅ν΅λ³μ(common variable)μ λν λμ μλ°μ΄νΈ(concurrent update) λλ¬Έμ λνλλ λ¬Έμ 

## π μκ³μμ­
### β Critical Section(μκ³μμ­)
- λ©ν° μ€λ λ©μ λ¬Έμ μ μμ λμ€λ―, λμΌν μμμ λμμ μ κ·Όνλ μμ(e.g. κ³΅μ νλ λ³μ μ¬μ©, λμΌ νμΌμ μ¬μ©νλ λ±)μ μ€ννλ μ½λ μμ­μ Critical Section μ΄λΌ μΉ­νλ€.

- μ μμ μμ κ³΅ν΅ λ³μλ κ³μ’μ μμ‘μ΄λ€. μ΄μ μ κ·Όνλ νλ‘μΈμ€μ μ½λλ₯Ό λ³΄λ©΄ λ€μκ³Ό κ°λ€. μ΄λ¬ν κ³΅ν΅λ³μ κ΅¬μ­μ μκ³κ΅¬μ­μ΄λΌκ³  νλ€.
``` java
void deposit(int amount) {
  balance = balance + amount; //μΆκΈ
}
void withdraw(int amount) {
  balance = balance - amount; //μκΈ
}
```

### βCritical Section Problem(μκ³μμ­ λ¬Έμ )
- νλ‘μΈμ€λ€μ΄ Critical Section μ ν¨κ» μ¬μ©ν  μ μλ νλ‘ν μ½μ μ€κ³νλ κ²μ΄λ€.

### β Requirements(ν΄κ²°μ μν κΈ°λ³Έμ‘°κ±΄)
- Mutual Exclusion(μνΈ λ°°μ )
  νλ‘μΈμ€ P1 μ΄ Critical Section μμ μ€νμ€μ΄λΌλ©΄, λ€λ₯Έ νλ‘μΈμ€λ€μ κ·Έλ€μ΄ κ°μ§ Critical Section μμ μ€νλ  μ μλ€.
- Progress(μ§ν)
  Critical Section μμ μ€νμ€μΈ νλ‘μΈμ€κ° μκ³ , λ³λμ λμμ΄ μλ νλ‘μΈμ€λ€λ§ Critical Section μ§μ νλ³΄λ‘μ μ°Έμ¬λ  μ μλ€.
- Bounded Waiting(νμ λ λκΈ°)
  P1 κ° Critical Section μ μ§μ μ μ²­ ν λΆν° λ°μλ€μ¬μ§ λκ°μ§, λ€λ₯Έ νλ‘μΈμ€λ€μ΄ Critical Section μ μ§μνλ νμλ μ νμ΄ μμ΄μΌ νλ€.



### β ν΄κ²°μ±
#### (1) Lock
- νλμ¨μ΄ κΈ°λ° ν΄κ²°μ±μΌλ‘μ¨, λμμ κ³΅μ  μμμ μ κ·Όνλ κ²μ λ§κΈ° μν΄ Critical Section μ μ§μνλ νλ‘μΈμ€λ Lock μ νλνκ³  Critical Section μ λΉ μ Έλμ¬ λ, Lock μ λ°©μΆν¨μΌλ‘μ¨ λμμ μ κ·Όμ΄ λμ§ μλλ‘ νλ€.

- νκ³
  λ€μ€μ²λ¦¬κΈ° νκ²½μμλ μκ°μ μΈ ν¨μ¨μ± μΈ‘λ©΄μμ μ μ©ν  μ μλ€.
#### (2) Semaphores(μΈλ§ν¬)
- μΈλ§ν¬λ λκΈ°νλ₯Ό μν΄ λ§λ€μ΄μ§ μννΈμ¨μ΄λ‘μ, λνμ μΈ λκΈ°ν λκ΅¬μ΄λ€.

- μννΈμ¨μ΄μμμ Critical Section λ¬Έμ λ₯Ό ν΄κ²°νκΈ° μν λκΈ°ν λκ΅¬

``` java
class Semaphore {
  int value;      // number of permits
  Semaphore(int value) {
    // ...
  }
  void acquire() {
    value--;
    if (value < 0) {
      // add this process/thread to list
      // block
    }
  }
  void release() {
    value++;
    if (value <= 0) {
      // remove a process P from list
      // wakeup P
    }
  }
}
```
μ μ½λμμ acquire() λ valueκ°μ κ°μμν€κ³  λ§μ½ valueκ°μ΄ 0λ³΄λ€ μμΌλ©΄ μ΄λ―Έ ν΄λΉ μκ³κ΅¬μ­μ μ΄λ νλ‘μΈμ€κ° μ‘΄μ¬νλ€λ μλ―Έμ΄λ―λ‘ νμ¬ νλ‘μΈμ€λ μ κ·Όνμ§ λͺ»νλλ‘ λ§μμΌνλ€. μ΄λ₯Ό listλΌλ κΈ°λ€λ¦¬λ μ€μ μΆκ°ν λ€ blockμ κ±Έμ΄μ€λ€.(listλ μΌλ°μ μΌλ‘ νλ‘ λμ΄μλ€.)

release() λ valueκ°μ μ¦κ°μν€κ³ , λ§μ½ valueκ°μ΄ 0λ³΄λ€ κ°κ±°λ μμΌλ©΄ μκ³κ΅¬μ­μ μ§μνλ €κ³  λκΈ°νλ νλ‘μΈμ€κ° listμ λ¨μμλ€λ μλ―Έμ΄λ―λ‘ κ·Έ μ€μμ νλλ₯Ό κΊΌλ΄μ΄ μκ³κ΅¬μ­μ μνν  μ μλλ‘ ν΄μ£Όμ΄μΌ νλ€.

![](https://images.velog.io/images/kcwthing1210/post/ba54b82d-d11c-4ec0-ba1e-65434cba7d96/image.png)
μΈλ§ν¬λ₯Ό κ·Έλ¦ΌμΌλ‘ λνλ΄λ©΄ μμ κ°λ€. listλ μ€μ λ‘ νλ‘ λ³Ό μ μλ€. acquire()μ μν΄ blockλλ νλ‘μΈμ€λ μΈλ§ν¬ λ΄λΆμ μλ νμ μ½μλ ν, λ€λ₯Έ νλ‘μΈμ€κ° μκ³κ΅¬μ­μ λμ€λ©΄μ release()λ₯Ό νΈμΆνμ¬ μΈλ§ν¬ νμ μλ νλ‘μΈμ€λ₯Ό κΉ¨μμΌ νλ€.(λ€μ ready queueλ‘ λ³΄λΈλ€.)

μμμ μ΄ν΄λ³Έ κ²μ²λΌ μΈλ§ν¬λ μΌλ°μ μΌλ‘ Mutual exclusionμ μν΄ μ¬μ©λλ€.

- ex )
  μ²μμ μ΄ν΄λ³Έ μνκ³μ’ λ¬Έμ μ μΈλ§ν¬λ₯Ό μ μ©ν΄λ³΄μ. μμμ μκ³κ΅¬μ­μ BankAccount ν΄λμ€ λ΄λΆμ μμΆλ ₯νλ λΆλΆμΈ κ²μ λ³΄μλ€. μ¬κΈ°μ μΈλ§ν¬λ₯Ό μ μ©ν΄λ³΄λ©΄ μλμ κ°λ€.
  μ΄λ, value κ°μ μκ³κ΅¬μ­μ λͺ κ°μ νλ‘μΈμ€λ₯Ό μ κ·Όν  κ²μΈμ§ μ νλ κ²κ³Ό κ°λ€. μ§κΈμ μκ³ κ΅¬μ­μ νλμ νλ‘μΈμ€λ§ μ κ·Όκ°λ₯νκΈ° λλ¬Έμ 1 λ‘ μ΄κΈ°ν νλ€.

``` java 
import java.util.concurrent.Semaphore;  // μΈλ§ν¬λ₯Ό μ¬μ©νκΈ° μν΄ νμΌ κ°μ₯ μμ μΆκ°ν΄μΌ νλ€.

class BankAccount {
	int balance;

	Semaphore sem;
	BankAccount() {   // BankAccount ν΄λμ€μ μμ±μκ° νΈμΆλλ©΄ μΈλ§ν¬λ₯Ό λ§λ λ€.
		sem = new Semaphore(1);  // value κ°μ 1λ‘ μ΄κΈ°ννλ€.
	}

	void deposit(int amount) {
		try {
			sem.acquire();   // μκ³κ΅¬μ­μ λ€μ΄κ°κΈ°λ₯Ό μμ²­νλ€.
		} catch (InterruptedException e) {}
	    /* μκ³ κ΅¬μ­ */  
		int temp = balance + amount;
		System.out.print("+");
		balance = temp;

		sem.release();   // μκ³κ΅¬μ­μμ λκ°λ€.
	}
	void withdraw(int amount) {
		try {
			sem.acquire();
		} catch (InterruptedException e) {}
	    /* μκ³ κ΅¬μ­ */  
		int temp = balance - amount;
		System.out.print("-");
		balance = temp;

		sem.release();
	}
	int getBalance() {
		return balance;
	}
}
```
- μΈλ§ν¬λ mutual exclusionλΏ μλλΌ orderingμ νκΈ° μν΄μλ μ¬μ©νλ€. μ¦, νλ‘μΈμ€μ μ€ν μμλ₯Ό μνλ μμλ‘ μ€μ  ν  μ μλ€.

![](https://images.velog.io/images/kcwthing1210/post/4e41bb58-1eb1-4a29-b504-0e7acbc0c081/image.png)

μλ₯Ό λ€μ΄, νλ‘μΈμ€κ° P1, P2 λ κ°κ° μλ€κ³  κ°μ νμ. μνλ μμλ P1, P2 μμΌλ‘ μ€ννκΈ°λ₯Ό μνλ€. κ·Έλ¬λ©΄ μλμ κ°μ΄ μ€μ ν΄μ€ μ μλ€.
λ¨Όμ , μΈλ§ν¬λ‘ κ°μΌ κ΅¬μ­μ λ€μ΄κ° μ μλ νλ‘μΈμ€ κ°μλ₯Ό μ νλ valueκ°μ 0μΌλ‘ μ€μ νλ€.
- sem value = 0;

1. P1μ΄ λ¨Όμ  μ€νλ κ²½μ°
   Section 1 μ΄μ μ μλ¬΄λ° λμμ΄ μμΌλ―λ‘ λ°λ‘ μννλ€.
   sem.release() λ₯Ό λ§λλ©΄ valueκ°μ 1 μ¦κ°μν€κ³ , μΈλ§ν¬ νμ μλ νλ‘μΈμ€λ₯Ό κΉ¨μμ£Όλλ° νμ¬μλ νμ νλ‘μΈμ€κ° μμΌλ―λ‘ μλ¬΄ λμλ νμ§ μλλ€.
   P2κ° μ€νλλ€.
   P2μ sem.acquire() λ₯Ό λ§λλ©΄ νμ¬ valueκ°μ 1μ΄κ³  μ΄λ₯Ό 1κ°μμν€λ©΄ 0μ΄ λλ€. value = 0μ΄λ©΄ blockμ νμ§ μμΌλ―λ‘, λ¬΄μ¬ν Section 2κ° μνλλ€.
2. P2κ° λ¨Όμ  μ€νλ κ²½μ°
   Section 2 μ΄μ μ sem.acquire() κ° μμΌλ―λ‘ μ΄λ₯Ό μννλλ°, νμ¬ valueκ°μ 0μ΄κ³  μ΄λ₯Ό 1 κ°μ μν€λ©΄ -1 μ΄ λλ€. valueκ°μ΄ μμλ©΄ ν΄λΉ νλ‘μΈμ€λ₯Ό blockμν¨λ€.(μΈλ§ν¬ νμ μ½μνλ€.)
   P1μ΄ μ€νλλ©΄ Section 1μ΄ λ°λ‘ μνλλ€.
   sem.release() λ₯Ό λ§λλ©΄ valueκ°μ 1 μ¦κ°μν€κ³ , μΈλ§ν¬ νμ μλ P2 νλ‘μΈμ€λ₯Ό κΉ¨μμ€λ€.(νμ¬ value = 0)
   P2μ Section 2κ° μνλλ€.
   μμμ λ κ°μ§ κ²½μ°λ₯Ό μ΄ν΄λ³΄μλ―μ΄, P1, P2 λ μ€ μ΄λ κ²μ λ¨Όμ  μ€ννμ¬λ κ²°κ³Όμ μΌλ‘ P1 -> P2 μμλ‘ μννλ κ²μ μ μ μλ€.

ex) java
```
class BankAccount {
	int balance;

	Semaphore sem, semOrder;
	BankAccount() {
		sem = new Semaphore(1);
		semOrder = new Semaphore(0);   // Ordeingμ μν μΈλ§ν¬
	}

	void deposit(int amount) {
		try {
			sem.acquire();
		} catch (InterruptedException e) {}
		int temp = balance + amount;
		System.out.print("+");
		balance = temp;
		sem.release();
		semOrder.release();   // blockλ μΆκΈ νλ‘μΈμ€κ° μλ€λ©΄ κΉ¨μμ€λ€.
	}
	void withdraw(int amount) {
		try {
			semOrder.acquire();   // μΆκΈμ λ¨Όμ νλ €κ³  νλ©΄ blockνλ€.
			sem.acquire();
		} catch (InterruptedException e) {}
		int temp = balance - amount;
		System.out.print("-");
		balance = temp;
		sem.release();
	}
	int getBalance() {
		return balance;
	}
}
```


- μ’λ₯
    - μΉ΄μ΄ν μΈλ§ν¬
      κ°μ©ν κ°μλ₯Ό κ°μ§ μμ μ λν μ κ·Ό μ μ΄μ©μΌλ‘ μ¬μ©λλ©°, μΈλ§ν¬λ κ·Έ κ°μ©ν μμμ κ°μ λ‘ μ΄κΈ°ν λλ€. μμμ μ¬μ©νλ©΄ μΈλ§ν¬κ° κ°μ, λ°©μΆνλ©΄ μΈλ§ν¬κ° μ¦κ° νλ€.
    - μ΄μ§ μΈλ§ν¬
      MUTEX λΌκ³ λ λΆλ₯΄λ©°, μνΈλ°°μ μ (Mutual Exclusion)μ λ¨Έλ¦ΏκΈμλ₯Ό λ°μ λ§λ€μ΄μ‘λ€. μ΄λ¦ κ·Έλλ‘ 0 κ³Ό 1 μ¬μ΄μ κ°λ§ κ°λ₯νλ©°, λ€μ€ νλ‘μΈμ€λ€ μ¬μ΄μ Critical Section λ¬Έμ λ₯Ό ν΄κ²°νκΈ° μν΄ μ¬μ©νλ€.

- λ¨μ 
    - Busy Waiting(λ°μ λκΈ°)
      Spin lockμ΄λΌκ³  λΆλ¦¬λ Semaphore μ΄κΈ° λ²μ μμ Critical Section μ μ§μν΄μΌνλ νλ‘μΈμ€λ μ§μ μ½λλ₯Ό κ³μ λ°λ³΅ μ€νν΄μΌ νλ©°, CPU μκ°μ λ­λΉνμλ€. μ΄λ₯Ό Busy Waitingμ΄λΌκ³  λΆλ₯΄λ©° νΉμν μν©μ΄ μλλ©΄ λΉν¨μ¨μ μ΄λ€. μΌλ°μ μΌλ‘λ Semaphoreμμ Critical Sectionμ μ§μμ μλνμ§λ§ μ€ν¨ν νλ‘μΈμ€μ λν΄ Blockμν¨ λ€, Critical Sectionμ μλ¦¬κ° λ  λ λ€μ κΉ¨μ°λ λ°©μμ μ¬μ©νλ€. μ΄ κ²½μ° Busy waitingμΌλ‘ μΈν μκ°λ­λΉ λ¬Έμ κ° ν΄κ²°λλ€.
    - Deadlock(κ΅μ°©μν)
      μΈλ§ν¬κ° Ready Queue λ₯Ό κ°μ§κ³  μκ³ , λ μ΄μμ νλ‘μΈμ€κ° Critical Section μ§μμ λ¬΄νμ  κΈ°λ€λ¦¬κ³  μκ³ , Critical Section μμ μ€νλλ νλ‘μΈμ€λ μ§μ λκΈ° μ€μΈ νλ‘μΈμ€κ° μ€νλμΌλ§ λΉ μ Έλμ¬ μ μλ μν©μ μ§μΉ­νλ€.


#### (3) λͺ¨λν°
κ³ κΈ μΈμ΄μ μ€κ³ κ΅¬μ‘°λ¬Όλ‘μ, κ°λ°μμ μ½λλ₯Ό μνΈλ°°μ  νκ²λ λ§λ  μΆμνλ λ°μ΄ν° ννμ΄λ€.
κ³΅μ μμμ μ κ·ΌνκΈ° μν ν€ νλκ³Ό μμ μ¬μ© ν ν΄μ λ₯Ό λͺ¨λ μ²λ¦¬νλ€. (μΈλ§ν¬μ΄λ μ§μ  ν€ ν΄μ μ κ³΅μ μμ μ κ·Ό μ²λ¦¬κ° νμνλ€. )


## π§© Reference
- https://private.tistory.com/24
- https://velog.io/@codemcd/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9COS-8.-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%8F%99%EA%B8%B0%ED%99%94-1#32-ordering

# π λ©λͺ¨λ¦¬ κ΄λ¦¬ μ λ΅

## πλ©λͺ¨λ¦¬ κ΄λ¦¬ λ°°κ²½
κ°κ°μ νλ‘μΈμ€ λ λλ¦½λ λ©λͺ¨λ¦¬ κ³΅κ°μ κ°κ³ , μ΄μμ²΄μ  νΉμ λ€λ₯Έ νλ‘μΈμ€μ λ©λͺ¨λ¦¬ κ³΅κ°μ μ κ·Όν  μ μλ μ νμ΄ κ±Έλ €μλ€. λ¨μ§, μ΄μμ²΄μ  λ§μ΄ μ΄μμ²΄μ  λ©λͺ¨λ¦¬ μμ­κ³Ό μ¬μ©μ λ©λͺ¨λ¦¬ μμ­μ μ κ·Όμ μ μ½μ λ°μ§ μλλ€.

## π νλ‘μΈμ€ λ°μΈλ©
νλ‘μΈμ€μ λ©λͺ¨λ¦¬ λ²μλ₯Ό κ²°μ νλ κ²μ λ°μΈλ©(Binding)μ΄λΌκ³  νλ©°, λ°μΈλ©μ μννλ μμ μ λ°λΌ λ€μκ³Ό κ°μ΄ λΆλ₯ν  μ μλ€.

### β Compile-Time Binding
- νλ‘κ·Έλ¨μ μ»΄νμΌ ν  λ λ©λͺ¨λ¦¬ λ²μλ₯Ό κ²°μ .
- λ²μκ° λ¬λΌμ§λ©΄ μ¬μ»΄νμΌ ν΄μΌνλ€.
- λ€λ₯Έ νλ‘κ·Έλ¨μ λ©λͺ¨λ¦¬ λ²μκ° κ²ΉμΉμ§ μλλ‘ νλ‘κ·Έλλ¨Έκ° μ£Όμν΄μΌ ν¨.
- λμ€ μμ μλ μ°λ λ°©μ.
### β Load-Time Binding
- νλ‘κ·Έλ¨μ΄ λ¨μ μ μ¬λκΈ° μ μ BASEμ LIMITμ κ²°μ .
- λ€λ₯Έ νλ‘κ·Έλ¨μ λ©λͺ¨λ¦¬ λ²μκ° κ²ΉμΉμ§ μλλ‘ μ΄μμ²΄μ κ° κ΄λ¦¬ν¨.
- νλ μμ€νμ μ±νλ¨.
### β Run-Time Binding
- μ€νμ€μ μ΄μμ²΄μ μ μν΄ λ€λ₯Έ λ©λͺ¨λ¦¬ μ£Όμλ‘ μ?κ²¨μ§ μ μμ.
- μ μ¬μκ° λ°μΈλ©μ κΈ°λ³Έμ μΌλ‘ ν¬ν¨ν¨.
- νΉμν νλμ¨μ΄κ° νμν¨.


## π μ€μν
### β μ μ
-  λ©λͺ¨λ¦¬μ κ΄λ¦¬λ₯Ό μν΄ μ¬μ©λλ κΈ°λ². νμ€ Swapping λ°©μμΌλ‘λ round-robin κ³Ό κ°μ μ€μΌμ€λ§μ λ€μ€ νλ‘κ·Έλλ° νκ²½μμ CPU ν λΉ μκ°μ΄ λλ νλ‘μΈμ€μ λ©λͺ¨λ¦¬λ₯Ό λ³΄μ‘° κΈ°μ΅μ₯μΉ(e.g. νλλμ€ν¬)λ‘ λ΄λ³΄λ΄κ³  λ€λ₯Έ νλ‘μΈμ€μ λ©λͺ¨λ¦¬λ₯Ό λΆλ¬ λ€μΌ μ μλ€.

### β νΉμ§
![](https://images.velog.io/images/kcwthing1210/post/4dcf5e67-41d9-4736-a17d-a0e613c23c1e/image.png)

- swap-in : μ£Ό κΈ°μ΅μ₯μΉ(RAM)μΌλ‘ λΆλ¬μ€λ κ³Όμ 
- swap-out : λ³΄μ‘° κΈ°μ΅μ₯μΉλ‘ λ΄λ³΄λ΄λ κ³Όμ 
- swap μλ ν° λμ€ν¬ μ μ‘μκ°μ΄ νμνκΈ° λλ¬Έμ νμ¬μλ λ©λͺ¨λ¦¬ κ³΅κ°μ΄ λΆμ‘±ν λ Swapping μ΄ μμλλ€.

### β λμ€ν¨μ²
- μ€μνμ μν΄ μμμ΄ λ©λͺ¨λ¦¬μ μ μ¬λμ΄ μμ§ μμ κ°λ₯μ±μ΄ μκ²ΌμΌλ―λ‘, μ€νν  μμμ΄ λ©λͺ¨λ¦¬ μ μ¬λμ΄ μλμ§ κ²μ¬νλ νλ‘κ·Έλ¨

- λ©λͺ¨λ¦¬μ μ μ¬λμ΄ μλμ§ κ²μ¬νκ³ , λ©λͺ¨λ¦¬μ μλ€λ©΄ μ΄λ―Έμ§λ₯Ό μ¬μ μ¬

### β λ¨μ 
- λ¬Έλ§₯κ΅ν λΉμ©μ μ¦κ°

κ³ μ μ  μ€μνμ λ³΄μ‘° κΈ°μ΅μ₯μΉμ μμμ λ°±μνκΈ° λλ¬Έμ, κΈ°μ΅μ₯μΉμ μλκ° λλ¦¬λ©΄ μ€μνμ μλλ κ°μ΄ λλ €μ‘μ΅λλ€. μ€μνμ λ¬Έλ§₯κ΅νμμ λ°μνλ―λ‘ λ¬Έλ§₯κ΅νμ λΉμ©μ΄ λν­ μ¦κ°ν κ²κ³Ό κ°μ΅λλ€. μ΄κ²μ μ§§μ μ£ΌκΈ°μ λΌμ΄λ λ‘λΉ μμ€νμμ λ§€μ° μΉλͺμ μλλ€.

- μμ€ν μ²λ¦¬μ¨ κ°μ :

κ·Έλ¦¬κ³  μ€μνμλ§ λ§€λ¬λ¦¬λ λ°λμ μμμ μνν  μκ°μ΄ λΆμ‘±νλ―λ‘ μμ€νμ μ²λ¦¬μ¨λ κ°μν©λλ€.

- μ¬λ°°μΉ μ΄μ :

μ€μνμ μν΄ λ³΄μ‘°κΈ°μ΅μ₯μΉλ‘ λ μκ° μμμ΄ λ€μ λμμμΌ ν  λ BASE λ μ§μ€ν°λ₯Ό μ΄λ»κ² ν κ²μΈμ§μ λν κ³ λ―Όλ νμν©λλ€. μ΄μ κ³Ό κ°μ μ₯μλ‘ λ°°μΉλλ€λ©΄ μ’κ² μ§λ§, ν­μ κ·Έκ²μ΄ λ³΄μ₯λμ΄ μλ κ²μ μλλλ€. Run-Time Bindingμ΄ νμ©λλ μμ€νμ΄λΌλ©΄ μ’κ² μ§λ§, λͺ¨λ  μμ€νμ΄ μ΄λ₯Ό μ§μνλ κ²λ μλλλ€.

## π λ©λͺ¨λ¦¬ ν λΉμ λΆλ₯
### β λ¨νΈν
- νλ‘μΈμ€λ€μ΄ λ©λͺ¨λ¦¬μ μ μ¬λκ³  μ κ±°λλ μΌμ΄ λ°λ³΅λλ€λ³΄λ©΄, νλ‘μΈμ€λ€μ΄ μ°¨μ§νλ λ©λͺ¨λ¦¬ ν μ¬μ΄μ μ¬μ© νμ§ λͺ»ν  λ§νΌμ μμ μμ κ³΅κ°λ€μ΄ λμ΄λκ² λλλ°, μ΄κ²μ΄ λ¨νΈν μ΄λ€. -

- μ’λ₯
    - μΈλΆ λ¨νΈν: λ©λͺ¨λ¦¬ κ³΅κ° μ€ μ¬μ©νμ§ λͺ»νκ² λλ μΌλΆλΆ. λ¬Όλ¦¬ λ©λͺ¨λ¦¬(RAM)μμ μ¬μ΄μ¬μ΄ λ¨λ κ³΅κ°λ€μ λͺ¨λ ν©μΉλ©΄ μΆ©λΆν κ³΅κ°μ΄ λλ λΆλΆλ€μ΄ λΆμ°λμ΄ μμλ λ°μνλ€κ³  λ³Ό μ μλ€.
    - λ΄λΆ λ¨νΈν: νλ‘μΈμ€κ° μ¬μ©νλ λ©λͺ¨λ¦¬ κ³΅κ° μ ν¬ν¨λ λ¨λ λΆλΆ. μλ₯Όλ€μ΄ λ©λͺ¨λ¦¬ λΆν  μμ  κ³΅κ°μ΄ 10,000B μκ³  Process A κ° 9,998B μ¬μ©νκ²λλ©΄ 2B λΌλ μ°¨μ΄ κ° μ‘΄μ¬νκ³ , μ΄ νμμ λ΄λΆ λ¨νΈνλΌ μΉ­νλ€.

### β μΈλΆ λ¨νΈν ν΄κ²°
-  μμΆ : μΈλΆ λ¨νΈνλ₯Ό ν΄μνκΈ° μν΄ νλ‘μΈμ€κ° μ¬μ©νλ κ³΅κ°λ€μ νμͺ½μΌλ‘ λͺ°μ, μμ κ³΅κ°μ νλ³΄νλ λ°©λ²λ‘  μ΄μ§λ§, μμν¨μ¨μ΄ μ’μ§ μλ€.
- μΈλΆ λ¨νΈνλ μ μ΄μ μ°μμ  ν λΉμμλ§ λ°μνλ―λ‘, λΉμ°μμ  ν λΉ λ°©μμΈ νμ΄μ§μ μ¬μ©νμ¬ μΈλΆ λ¨νΈνλ₯Ό λ°©μ§

### β μ°μμ  λ©λͺ¨λ¦¬ ν λΉ

#### (1) κ³ μ  ν¬κΈ° ν λΉ
![](https://images.velog.io/images/kcwthing1210/post/d71561b2-e3e2-49eb-b4b6-7f01f80ec502/image.png)

- λ©λͺ¨λ¦¬λ₯Ό λμΌν ν¬κΈ°λ‘ μλ₯Έ λ€, κ° νλ‘μΈμ€λ§λ€ λΈλ­ νλλ§ μ£Όλ λ°©μ
- μ μ²΄ λ©λͺ¨λ¦¬κ° NλΆν  λμλ€λ©΄ μ μ¬λ  μ μλ νλ‘μΈμ€λ μ΅λ Nκ°μ΄λ―λ‘ λ€μ€ νλ‘κ·Έλλ° μ λλ λΈλ­μ κ°μμ κ°μΌλ©°, λͺ¨λ  νλ‘μΈμ€λ ν λΉλ λ©λͺ¨λ¦¬ ν¬κΈ°κ° μλ‘ κ°λ€.
- νλμμλ μ¬μ©λμ§ μλ λ°©μ



#### (2) λμ  ν¬κΈ° ν λΉ
![](https://images.velog.io/images/kcwthing1210/post/0804a81a-d69f-4754-b17f-2c405b4179f7/image.png)
- κ³ μ  ν λΉκ³Ό λ¬λ¦¬ κ° νλ‘μΈμ€μκ² ν λΉλ λ©λͺ¨λ¦¬ ν¬κΈ°κ° λ€λ₯Ό μμ
- κ³ μ  ν λΉκ³Ό λ¬λ¦¬ ν λΉκ³Ό ν΄μ λ₯Ό λ°λ³΅νλ€λ³΄λ©΄, μ€κ°μ€κ°μ μκΈ°λ μ λλ‘ μ¬μ©ν  μ μλ λΉ κ³΅κ°μΈ μΈλΆ λ¨νΈν(External Fragmentation)λΌλ λ¬Έμ λ₯Ό λ°μ
- κ°κ°μ λ¨νΈνμ ν¬κΈ°λ μμμ§λΌλ, μ λΆ λͺ¨μΌλ©΄ μλ‘μ΄ νλ‘μΈμ€λ₯Ό νλ λ μ μ¬ν  μ μμλ§νΌ μ»€μ§κΈ° λλ¬Έμ λμ  ν λΉμ κ³ μ§μ μΈ λ¨μ 
- μ’λ₯
  - μ΅μ΄ μ ν©
  ![](https://images.velog.io/images/kcwthing1210/post/d780e61c-33e1-4483-8fc7-ef2dbc63599d/image.png)
    - μ²μμΌλ‘ λ§λ μ λΉν λΉ κ³΅κ°μ νλ‘μΈμ€λ₯Ό μ μ¬
    - μ²μμΌλ‘ λ§λ λΉ κ³΅κ°μ λ°λ‘ ν λΉν΄μ£Όλ©΄ λλ―λ‘, λ€λ₯Έ λ λ°©μλ³΄λ€ μκ°λ³΅μ‘λκ° λ?μ

    - μ΅μ  μ ν©
    ![](https://images.velog.io/images/kcwthing1210/post/4a562079-0661-4325-b08f-2ede04bea57f/image.png)
    	- μ΅μ  μ ν©(Best-Fit)μ μ λΉν λΉ μ¬λ‘― μ€ κ°μ₯ μμ κ³΅κ°μ νλ‘μΈμ€λ₯Ό μ μ¬
        - λͺ¨λ  λΉ κ³΅κ°μ νμν΄μΌ νλ―λ‘ μκ°λ³΅μ‘λκ° λμΌλ©°, λ§€μ° μμ ν¬κΈ°μ λΉκ³΅κ°μ μμ±
    
    - μ΅μ μ ν©
    ![](https://images.velog.io/images/kcwthing1210/post/02998eb2-775b-4885-85e9-5d7085cc47f6/image.png)
    	- μ λΉν λΉ μ¬λ‘― μ€ κ°μ₯ ν° κ³΅κ°μ νλ‘μΈμ€λ₯Ό μ μ¬ 
        - λͺ¨λ  λΉ κ³΅κ°μ νμν΄μΌ νλ―λ‘ μκ°λ³΅μ‘λκ° λμΌλ©°, λ§€μ° ν° ν¬κΈ°μ λΉκ³΅κ°μ μμ±




### β λΉμ°μμ  λ©λͺ¨λ¦¬ ν λΉ
#### Paging(νμ΄μ§)
- νλμ νλ‘μΈμ€κ° μ¬μ©νλ λ©λͺ¨λ¦¬ κ³΅κ°μ΄ μ°μμ μ΄μ΄μΌ νλ€λ μ μ½μ μμ λ λ©λͺ¨λ¦¬ κ΄λ¦¬ λ°©λ²μ΄λ€.
- μΈλΆ λ¨νΈνμ μμΆ μμμ ν΄μ νκΈ° μν΄ μκΈ΄ λ°©λ²λ‘ μΌλ‘, λ¬Όλ¦¬ λ©λͺ¨λ¦¬λ Frame μ΄λΌλ κ³ μ  ν¬κΈ°λ‘ λΆλ¦¬λμ΄ μκ³ , λΌλ¦¬ λ©λͺ¨λ¦¬(νλ‘μΈμ€κ° μ μ νλ)λ νμ΄μ§λΌ λΆλ¦¬λ κ³ μ  ν¬κΈ°μ λΈλ‘μΌλ‘ λΆλ¦¬λλ€.(νμ΄μ§ κ΅μ²΄ μκ³ λ¦¬μ¦μ λ€μ΄κ°λ νμ΄μ§)

- νμ΄μ§ κΈ°λ²μ μ¬μ©ν¨μΌλ‘μ¨ λΌλ¦¬ λ©λͺ¨λ¦¬λ λ¬Όλ¦¬ λ©λͺ¨λ¦¬μ μ μ₯λ  λ, μ°μλμ΄ μ μ₯λ  νμκ° μκ³  λ¬Όλ¦¬ λ©λͺ¨λ¦¬μ λ¨λ νλ μμ μ μ ν λ°°μΉλ¨μΌλ‘ μΈλΆ λ¨νΈνλ₯Ό ν΄κ²°ν  μ μλ ν° μ₯μ μ΄ μλ€.

- νλμ νλ‘μΈμ€κ° μ¬μ©νλ κ³΅κ°μ μ¬λ¬κ°μ νμ΄μ§λ‘ λλμ΄μ κ΄λ¦¬λκ³ (λΌλ¦¬ λ©λͺ¨λ¦¬μμ), κ°λ³ νμ΄μ§λ μμμ μκ΄μμ΄ λ¬Όλ¦¬ λ©λͺ¨λ¦¬μ μλ νλ μμ mapping λμ΄ μ μ₯λλ€κ³  λ³Ό μ μλ€.

- λ¨μ  : λ΄λΆ λ¨νΈν λ¬Έμ μ λΉμ€μ΄ λμ΄λκ² λλ€. μλ₯Όλ€μ΄ νμ΄μ§ ν¬κΈ°κ° 1,024B μ΄κ³  νλ‘μΈμ€ A κ° 3,172B μ λ©λͺ¨λ¦¬λ₯Ό μκ΅¬νλ€λ©΄ 3 κ°μ νμ΄μ§ νλ μ(1,024 * 3 = 3,072) νκ³ λ 100B κ° λ¨κΈ°λλ¬Έμ μ΄ 4 κ°μ νμ΄μ§ νλ μμ΄ νμν κ²μ΄λ€. κ²°λ‘ μ μΌλ‘ 4 λ²μ§Έ νμ΄μ§ νλ μμλ 924B(1,024 - 100)μ μ¬μ  κ³΅κ°μ΄ λ¨κ² λλ λ΄λΆ λ¨νΈν λ¬Έμ κ° λ°μνλ κ²μ΄λ€.


#### Segmentation(μΈκ·Έλ©νμ΄μ)
- νμ΄μ§μμμ²λΌ λΌλ¦¬ λ©λͺ¨λ¦¬μ λ¬Όλ¦¬ λ©λͺ¨λ¦¬λ₯Ό κ°μ ν¬κΈ°μ λΈλ‘μ΄ μλ, μλ‘ λ€λ₯Έ ν¬κΈ°μ λΌλ¦¬μ  λ¨μμΈ μΈκ·Έλ¨ΌνΈ(Segment)λ‘ λΆν  μ¬μ©μκ° λ κ°μ μ£Όμλ‘ μ§μ (μΈκ·Έλ¨ΌνΈ λ²νΈ + λ³μ) μΈκ·Έλ¨ΌνΈ νμ΄λΈμλ κ° μΈκ·Έλ¨ΌνΈμ κΈ°μ€(μΈκ·Έλ¨ΌνΈμ μμ λ¬Όλ¦¬ μ£Όμ)κ³Ό νκ³(μΈκ·Έλ¨ΌνΈμ κΈΈμ΄)λ₯Ό μ μ₯

- λ¨μ  : μλ‘ λ€λ₯Έ ν¬κΈ°μ μΈκ·Έλ¨ΌνΈλ€μ΄ λ©λͺ¨λ¦¬μ μ μ¬λκ³  μ κ±°λλ μΌμ΄ λ°λ³΅λλ€ λ³΄λ©΄, μμ  κ³΅κ°λ€μ΄ λ§μ μμ μμ μ‘°κ°λ€λ‘ λλμ΄μ Έ λͺ» μ°κ² λ  μλ μλ€.(μΈλΆ λ¨νΈν)


## π§© Reference
- https://aerocode.net/389#%ED%8E%98%EC%9D%B4%EC%A7%80-%ED%85%8C%EC%9D%B4%EB%B8%94-%EA%B5%AC%EC%A1%B0
 
