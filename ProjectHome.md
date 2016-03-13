# Pipeline Pattern #
Pipeline Pattern is helpful in dividing the problem into smaller reusable code components. This is a simple yet powerful **structural** pattern to organize a complex logic into smaller reusable components, which can be added/removed/modified independently.

---

The library and source code (in Java) for pipeline pattern and samples are under [downloads](http://code.google.com/p/pipelinepattern/downloads/list). Any comments or improvements, please contact Benoy Antony at bantony@gmail.com.

---

## Forces for the Pattern ##
**The logic is complex.**

**The simplicity and readability of the code is critical.**

**The logic can be divided into multiple modules.**

**The modules are potentially reusable for different usecases.**

## Description of the Pattern ##

**Stage** represents a module or work unit. The stage can be reused in different pipelines.
Stages collaborate with each other bay sharing data in the Context

**Pipeline** holds a collection of stages and executes them. Pipeline contains normal stages , error stages and final stages. Normal stages are executed. In case of any error, the execution of normal stages is stopped and error stages are executed. After this, final stages are executed. The error and final stages are optional.

**Context** acts as the holder class to share data between client and pipeline and also among stages.

**Client** setups the Pipeline by adding stages during init time and then executes pipeline by setting up the context.


## Sample Code illustrating usage of Pipeline Pattern ##

```

/**
 * A sample client class to demonstrate the usage of Pipeline Pattern
 * 
 * Takes an array of integers as input and does the following 
 * calculate the sum of all numbers
 * Increase each value in the array by adding the sum
 * sort the numbers
 * the sorted list is returned
 * @author Benoy Antony (benoy@ideaimpl.com) (http://www.ideaimpl.com)
 *
 */

public class NumberMagicWithSum {
	
	private static  final Pipeline S_PIPELINE = new SequentialPipeline();
	
	static{
		S_PIPELINE.addStage(new GetSumStage ());
		S_PIPELINE.addStage(new IncreaseValueStage ());
		S_PIPELINE.addStage(new SortStage ());
	}
	
	
	
	public int[]  doMagic(int[] numbers){
		NumberMagicContext nmContext = new NumberMagicContext ();
		nmContext.setInput(numbers);
		S_PIPELINE.execute(nmContext);
		return nmContext.getSortedValues();
	}
	
}
```

## Another Sample reusing some of the stages in the previous sample ##

```


/**
 * A sample client class to demonstrate the usage of Pipeline Pattern
 * 
 * Takes an array of integers as input and does the following 
 * calculate the product of all numbers
 * Increase each value in the array by adding the product
 * sort the numbers
 * the sorted list is returned
 * @author Benoy Antony (benoy@ideaimpl.com) (http://www.ideaimpl.com)
 *
 */

public class NumberMagicWithProduct {
	
	private static  final Pipeline S_PIPELINE = new SequentialPipeline();
	
	static{
		S_PIPELINE.addStage(new GetProductStage ());
		S_PIPELINE.addStage(new IncreaseValueStage ());
		S_PIPELINE.addStage(new SortStage ());
	}
	
	
	
	public int[]  doMagic(int[] numbers){
		NumberMagicContext nmContext = new NumberMagicContext ();
		nmContext.setInput(numbers);
		S_PIPELINE.execute(nmContext);
		return nmContext.getSortedValues();
	}

}

```


## Related Patterns ##
**Composite** pattern can be used to represent the relation between stages and pipeline. The Pipeline itself can be a stage and can become the stage in another pipeline.

## References ##
[This paper](http://www.cise.ufl.edu/research/ParallelPatterns/PatternLanguage/AlgorithmStructure/Pipeline.htm) formally defines theory of Pipeline Pattern.