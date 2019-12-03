## 30 包含min函数的栈

#### 题目：

定义栈的数据结构，请在该类型中实行一个能够得到栈的最小值的min函数。在该栈中，调用min、push、pop的时间复杂度都是O(1)。

#### 解题：

栈要求先进后出，如果实现了这个min()，也要求满足这个性质，否则不叫栈。

- 设立一个辅助栈，每次push最小值。如果数据栈要添加的元素大于最小值，那么还是push最小值。



```java
public class StackWithMin {

	Stack<Integer> stack_data = new Stack<Integer>();
	Stack<Integer> stack_min = new Stack<Integer>();
	
	//增加
	public void push(int value) {
		stack_data.push(value);
		if(stack_min.isEmpty() || stack_min.peek()>value) {
			stack_min.push(value);
		}else {
			stack_min.push(stack_min.peek());
		}
	}
	
	
	//弹出
	public void pop() {
		if(!stack_data.isEmpty()) {
			stack_data.pop();
			stack_min.pop();
		}else {
			System.out.println("栈已经空了，不能pop了");
		}
	}
	
	
	//求最小值
	public int min() {
		return stack_min.peek();
	}
	
}

```

