# Call By Value

```
public class CallByValue {
    public static void main(String[] args) {
        int a = 10;
        int b = a;
        
        b = 20;
        
        System.out.println(a);  // 10
        System.out.println(b);  // 20
    }
}
```

# Call By Reference

```
public class CallByValue {
    public static void main(String[] args) {
        Animal refA = new Animal();
        Animal refB = refA;
        
        refA.age = 10;
        refB.age = 20;
        
        System.out.println(refA.age);  // 20
        System.out.println(refB.age);  // 20
    }
}

class Animal {
    public int age;
}
```