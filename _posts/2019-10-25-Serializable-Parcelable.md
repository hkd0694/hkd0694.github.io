---
title:  "[Android] Serializable vs Parcelable"
excerpt: "Serializable과 Parcelable의 사용법과 차이점을 알아보자."
last_modified_at: 2019-10-25T08:06:00-05:00
 #categories:
 #  - Blog
 #tags:
 #  - Blog
---

## Serializable vs Parcelable

안드로이드 앱을 개발할 때 액티비티간 데이터를 전달하는 과정에서 인텐트에 전달할 데이터를 추가하게 됩니다.

하지만, 복잡한 클래스의 객체를 인텐트로 전달할 경우에 Serializable 또는 Parcelable를 사용하여 직렬화를 통해 인텐트에 추가해야 합니다.

>## Serializable이란?

Serializable 이란 Java 표준 인터페이스로, Serializable를 구현한 클래스 객체는 다른 액티비티로 이동할 준비가 되었다고 할 수 있다.

이 인터페이스를 사용하는 것은 정말 간단하다.

```java

import java.io.Serializable;

public class Model implements Serializable {
    
    private String name;
    private int age;
    private String description;

    public String getName() { return name; }

    public void setName(String name) { this.name = name; }

    public int getAge() { return age; }

    public void setAge(int age) { this.age = age; }

    public String getDescription() { return description; }

    public void setDescription(String description) { this.description = description; }
}
```

정말 간단하게도 전달하고자 하는 클래스에 Serializable만 implements만 해준다면 Model 객체를 다른 액티비티에게 전달할 수 있게 됩니다.

하지만 Serializable 은 내부에서 Reflection을 사용해서 직렬화를 처리합니다. Reflection은 프로세스 동작 중에 사용되며 처리 과정 중에 많은 추가 객체를 생성 합니다. 이 많은 쓰레기들은 가비지 컬렉터의 타겟이 되고 가비지 컬렉터의 과도한 동작으로 인하여 성능 저하 및 배터리 소모가 발생하게 됩니다.

>## Parcelable이란?

Serializable은 Java 표준 인터페이스라면 Parcelable은 Android SDK의 표준 인터페이스입니다.

Parcelable은 내부에서 Reflection을 사용하지 않도록 설계되었고, Serializable 과는 달리 직렬화 처리 방법을 사용자가 명시적으로 작성하기 때문에 Reflection이 필요 없습니다.

다음은 Parcelable 인터페이스의 사용법입니다.

```java

import android.os.Parcel;
import android.os.Parcelable;

import java.io.Serializable;

public class Model implements Parcelable {

    private String name;
    private int age;
    private String description;

    public Model(String name, int age, String description) {
        this.name = name;
        this.age = age;
        this.description = description;
    }

    public String getName() { return name; }

    public void setName(String name) { this.name = name; }

    public int getAge() { return age; }

    public void setAge(int age) { this.age = age; }

    public String getDescription() { return description; }

    public void setDescription(String description) { this.description = description; }

    protected Model(Parcel in) {
        this.name = in.readString();
        this.age = in.readInt();
        this.description = in.readString();
    }

    @Override
    public int describeContents() {
        return 0;
    }

    @Override
    public void writeToParcel(Parcel parcel, int i) {
        parcel.writeString(this.name);
        parcel.writeInt(this.age);
        parcel.writeString(this.description);
    }

    public static final Parcelable.Creator<Model> CREATOR = new Parcelable.Creator<Model>(){
        
        @Override
        public Model createFromParcel(Parcel source) { return new Model(source); }

        @Override
        public Model[] newArray(int i) { return new Model[i]; }
    };
}

```

Serializable 와는 달리 Parcelable은 구현해줘야 할 필수 메서드를 가지고 있고, 이는 클래스를 이해하기 어려우며, 새로운 기능을 추가하기 힘들게 만듭니다. 또한 코드의 추가로 클래스가 복잡해 질수록 유지 보수가 어려워지는 원인이 됩니다.

Serializable 이 시스템 비용이 발생하여 성능문제가 발생한다면 Parcelable은 구현과, 유지, 보수에 드는 사용자의 노력을 비용으로 지불해야 합니다.

>## 정리 (Serializable VS Parcelable)

Serializable의 장,단점

- 장점 : 마커 인터페이스이기 때문에 사용자가 사용하기 쉽다.
- 단점 : 시스템적인 비용이 비싸다. (내부적으로 Reflection이 사용됨.)

Parcelable의 장,단점

- 장점 : 시스템적인 부담이 적으며 빠르고, 직렬화 처리 방법을 사용자가 직접 작성하므로 내부적인 Reflection이 필요없다.
- 단점 : 유지 보수가 어려워짐.
