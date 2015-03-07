Android���ģʽԴ�����֮Proxyģʽ 
====================================
> ����Ϊ [Android ���ģʽԴ�����](https://github.com/simple-android-framework-exchange/android_design_patterns_analysis) �� Proxyģʽ ����  
> Androidϵͳ�汾�� 5.0       
> �����ߣ�[singwhatiwanna](https://github.com/singwhatiwanna)������״̬����ɣ�У���ߣ�[Mr.Simple](https://github.com/bboyfeiyu)��У��״̬�����     

#Binder�еĴ���ģʽ

��˵Binder�еĴ���ģʽ֮ǰ��������Ҫ�ȿ�������ģʽ�ļ�ʵ�֣���һ�������ݲ�����[��JAVA��ģʽ��֮����ģʽ](http://www.cnblogs.com/java-my-life/archive/2012/04/23/2466712.html)��ƪ�����еĴ���ʾ����uml��ͼ��

## 1. ģʽ����  
����ģʽ�Ƕ���Ľṹģʽ������ģʽ��ĳһ�������ṩһ��������󣬲��ɴ��������ƶ�ԭ��������á�

### ģʽ��ʹ�ó���
����һ���˻��߻���������һ���˻��߻�����ȡ�ж�����һЩ����£�һ���ͻ�������߲��ܹ�ֱ������һ�����󣬶������������ڿͻ��˺�Ŀ�����֮�����н�����á�

## 2. UML��ͼ
![url](images/proxy-uml.png)

### ��ɫ����
*��������ɫ��������Ŀ�����ʹ������Ĺ�ͬ�ӿڣ�����һ�����κο���ʹ��Ŀ�����ĵط�������ʹ�ô������
*Ŀ������ɫ�������˴�������������Ŀ�����
*��������ɫ����������ڲ�����Ŀ���������ã��Ӷ��������κ�ʱ�����Ŀ����󣻴�������ṩһ����Ŀ�������ͬ�Ľӿڣ��Ա�������κ�ʱ�����Ŀ����󡣴������ͨ���ڿͻ��˵��ô��ݸ�Ŀ�����֮ǰ��֮��ִ��ĳ�������������ǵ����ؽ����ô��ݸ�Ŀ�����

## 3. ģʽ�ļ�ʵ��
###  ��ʵ�ֵĽ���
����ͨ��һ�ֳ���ķ�ʽ��ʵ���´���ģʽ

### ʵ��Դ��
��������ɫ

```
public abstract class AbstractObject {
    //����
    public abstract void operation();
}
```

Ŀ������ɫ
```
public class RealObject extends AbstractObject {
    @Override
    public void operation() {
        //һЩ����
        System.out.println("һЩ����");
    }
}
```

��������ɫ
```
public class ProxyObject extends AbstractObject{
    RealObject realObject = new RealObject();
    @Override
    public void operation() {
        //����Ŀ�����֮ǰ��������ز���
        System.out.println("before");        
        realObject.operation();        
        //����Ŀ�����֮���������ز���
        System.out.println("after");
    }
}
```

�ͻ���
```
public class Client {
    public static void main(String[] args) {
        AbstractObject obj = new ProxyObject();
        obj.operation();
    }
}
```
## 4. ����ģʽ��Binder�е�ʹ��
ֱ����˵��Binder��Android�е�һ���࣬���̳���IBinder�ӿڡ���IPC�Ƕ���˵��Binder��Android�е�һ�ֿ����ͨ�ŷ�ʽ��Binder���������Ϊһ������������豸�������豸������/dev/binder����ͨ�ŷ�ʽ��linux��û�У���Android Framework�Ƕ���˵��Binder��ServiceManager���Ӹ���Manager��ActivityManager��WindowManager��etc������ӦManagerService����������AndroidӦ�ò���˵��Binder�ǿͻ��˺ͷ���˽���ͨ�ŵ�ý�飬����bindService��ʱ�򣬷���˻᷵��һ�������˷����ҵ����õ�Binder����ͨ�����Binder���󣬿ͻ��˾Ϳ��Ի�ȡ������ṩ�ķ���������ݣ�����ķ��������ͨ����ͻ���AIDL�ķ���

Binderһ������Ҫ�������ǣ����ͻ��˵��������ͨ��Parcel��װ�󴫵�Զ�̷���ˣ�Զ�̷���˽������ݲ�ִ�ж�Ӧ�Ĳ�����ͬʱ�ͻ����̹߳��𣬵�����˷���ִ����Ϻ��ٽ����ؽ��д�뵽����һ��Parcel�в�����ͨ��Binder���ص��ͻ��ˣ��ͻ��˽��յ��������ݵ�Parcel��Binder��������ݰ��е����ݲ���ԭʼ������ظ��ͻ��ˣ����ˣ�����Binder�Ĺ������̾�����ˡ��ɴ˿ɼ���Binder����һ������ͨ����Parcel����������ͨ���п���̴��䣬����˫�����ͨ�ţ��Ⲣ������ֻ��Ҫ˫������Լ���õĹ淶ȥ����ͽ�����ݼ��ɡ�

Ϊ�˸��õ�˵��Binder�������������ֶ���һ��Binder��Ϊ��ʹ���߼��������������һ�£�������ģ��һ������ϵͳ����������ṩ�Ĺ���ֻ��һ��������ѯ��ֻ�д���һ��int��id���������оͻὫ����������Ϊid*10�������´�ҵķ����Ρ�

1. �ȶ���һ��Binder�ӿ�
 ```
package com.ryg.design.manualbinder;

import android.os.IBinder;
import android.os.IInterface;
import android.os.RemoteException;

public interface IBank extends IInterface {

    static final String DESCRIPTOR = "com.ryg.design.manualbinder.IBank";

    static final int TRANSACTION_queryMoney = (IBinder.FIRST_CALL_TRANSACTION + 0);

    public long queryMoney(int uid) throws RemoteException;

}
```

2.����һ��Binder��ʵ����������ӿ�
```
package com.ryg.design.manualbinder;

import android.os.Binder;
import android.os.IBinder;
import android.os.Parcel;
import android.os.RemoteException;

public class BankImpl extends Binder implements IBank {

    public BankImpl() {
        this.attachInterface(this, DESCRIPTOR);
    }

    public static IBank asInterface(IBinder obj) {
        if ((obj == null)) {
            return null;
        }
        android.os.IInterface iin = obj.queryLocalInterface(DESCRIPTOR);
        if (((iin != null) && (iin instanceof IBank))) {
            return ((IBank) iin);
        }
        return new BankImpl.Proxy(obj);
    }

    @Override
    public IBinder asBinder() {
        return this;
    }

    @Override
    public boolean onTransact(int code, Parcel data, Parcel reply, int flags)
            throws RemoteException {
        switch (code) {
        case INTERFACE_TRANSACTION: {
            reply.writeString(DESCRIPTOR);
            return true;
        }
        case TRANSACTION_queryMoney: {
            data.enforceInterface(DESCRIPTOR);
            int uid = data.readInt();
            long result = this.queryMoney(uid);
            reply.writeNoException();
            reply.writeLong(result);
            return true;
        }
        }
        return super.onTransact(code, data, reply, flags);
    }

    @Override
    public long queryMoney(int uid) throws RemoteException {
        return uid * 10l;
    }

    private static class Proxy implements IBank {
        private IBinder mRemote;

        Proxy(IBinder remote) {
            mRemote = remote;
        }

        @Override
        public IBinder asBinder() {
            return mRemote;
        }

        public java.lang.String getInterfaceDescriptor() {
            return DESCRIPTOR;
        }

        @Override
        public long queryMoney(int uid) throws RemoteException {
            Parcel data = Parcel.obtain();
            Parcel reply = Parcel.obtain();
            long result;
            try {
                data.writeInterfaceToken(DESCRIPTOR);
                data.writeInt(uid);
                mRemote.transact(TRANSACTION_queryMoney, data, reply, 0);
                reply.readException();
                result = reply.readLong();
            } finally {
                reply.recycle();
                data.recycle();
            }
            return result;
        }

    }

}
```
ok������Ϊֹ�����ǵ�Binder������ˣ�����ֻҪ��������˺Ϳͻ��ˣ����߾���ͨ�����ǵ�Binder��ͨ���ˡ�����Ͳ������ʾ���ˣ����ǵ�Ŀ���Ƿ�������ģʽ��Binder�е�ʹ�á�

���ǿ�����Binder��ʵ���У���һ��������Proxy�����࣬���Ĺ��췽�����£�
```
  Proxy(IBinder remote) {
      mRemote = remote;
  }
```
Proxy�����һ��IBinder�������������ʵ���Ͼ��Ƿ����Service�е�onBind�������ص�Binder�����ڿͻ������´����Ľ������Ϊ�ͻ����޷�ֱ��ͨ����������Binder�ͷ����ͨ�ţ���˿ͻ��˱������Proxy�����ͷ����ͨ�ţ�����Proxy�����þ��Ǵ�������ã��ͻ������е�����ȫ��ͨ��Proxy���������幤������Ϊ��Proxy���յ�����˵�����󣬻Ὣ�ͻ��˵�������������Parcel�����У�Ȼ��Parcel����ͨ�����ڲ����е�Ibinder�����͵�����ˣ�����˽������ݡ�ִ�з����󷵻ؽ�����ͻ��˵�Proxy��Proxy�������ݺ󷵻ظ��ͻ��˵����������ߡ�����Ȼ�������������ľ��ǵ��͵Ĵ���ģʽ������Binder��δ������ݣ����漰���ܵײ��֪ʶ��������Ѹ㶮���������ݴ���ĺ���˼���ǹ����ڴ档

## 5. ��̸
### �ŵ���ȱ��
#### �ŵ�  
* �����������˱��ػ�����չ�ԣ������˴�ȡ��������

#### ȱ�� 
* ���������Ĵ�����