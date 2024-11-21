
# subsystem的蓝图子类

subsystem子类必须是C++声明，但是修改就比较麻烦，所以一般可以C++声明抽象类且蓝图可以调用，然后用蓝图继承此subsystem使用
![[Pasted image 20241121091044.png]]

然后就可以直接创建subsystem蓝图子类
![[Pasted image 20241121091431.png]]

就可以直接获取了
![[Pasted image 20241121091504.png]]



# **EditorSubsystem****

如果是**EditorSubsystem**，需要在Build.cs中添加EditorSubsystem模块并且需要实现3个函数
```C++
UCLASS(Abstract)
class ENGINE_API USubsystem : public UObject
{
	GENERATED_BODY()

public:
	USubsystem();

	/** Override to control if the Subsystem should be created at all.
	 * For example you could only have your system created on servers.
	 * It's important to note that if using this is becomes very important to null check whenever getting the Subsystem.
	 *
	 * Note: This function is called on the CDO prior to instances being created!
	 *
	 */
//需要重载的3个函数
	virtual bool ShouldCreateSubsystem(UObject* Outer) const { return true; }

	/** Implement this for initialization of instances of the system */
	virtual void Initialize(FSubsystemCollectionBase& Collection) {}

	/** Implement this for deinitialization of instances of the system */
	virtual void Deinitialize() {}

	/** Overridden to check global network context */
	virtual int32 GetFunctionCallspace(UFunction* Function, FFrame* Stack) override;

private:
	friend class FSubsystemCollectionBase;
	FSubsystemCollectionBase* InternalOwningSubsystem;

};
```


5种subsystem，生命周期不同，默认能调用的地方也是不同的

**EditorSubsystem，不能在关卡蓝图中调用，能在Edit Widget中调用**