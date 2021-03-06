# Pass<a name="amazon-states-language-pass-state"></a>

A `Pass` state \(`"Type": "Pass"`\) simply passes its input to its output, performing no work\. `Pass` states are useful when constructing and debugging state machines\.

In addition to the [common state fields](amazon-states-language-states.md#amazon-states-language-common-fields), `Pass` states allow the following fields:

** `Result` \(Optional\)**  
Treated as the output of a virtual task to be passed on to the next state, and filtered as prescribed by the `ResultPath` field \(if present\)\.

** `ResultPath` \(Optional\)**  
Specifies where \(in the input\) to place the "output" of the virtual task specified in `Result`\. The input is further filtered as prescribed by the `OutputPath` field \(if present\) before being used as the state's output\. For more information, see [Input and Output Processing](amazon-states-language-input-output-processing.md)\.

Here is an example of a `Pass` state that injects some fixed data into the state machine, probably for testing purposes\.

```
"No-op": {
  "Type": "Pass",
  "Result": {
    "x-datum": 0.381018,
    "y-datum": 622.2269926397355
  },
  "ResultPath": "$.coords",
  "Next": "End"
}
```

Suppose the input to this state is:

```
{
  "georefOf": "Home"
}
```

Then the output would be:

```
{
  "georefOf": "Home",
  "coords": {
    "x-datum": 0.381018,
    "y-datum": 622.2269926397355
  }
}
```