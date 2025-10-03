# Test Categories for Eager and Verbose Smell Detection

## Definitions

Based on the previous analysis and script definitions:

- **Eager Smell**: Production Method Call Count >= 4
- **Verbose Smell**: Lines of Code (LOC) >= 13  
- **DAT Smell**: Assertion Pasta (duplicate assertion testing)


## Notes

- These categories are mutually exclusive within each smell type comparison (Eager vs DAT, Verbose vs DAT)
- All examples were extracted from actual test files in the subject projects directory



## Concrete Test Method Examples

### Eager Smell Examples

#### 1. **Only Eager Smell Example**
**File:** `Activiti/APIProcessInstanceConverterTest.java`
**Method:** `should_convertFromInternalProcessInstance_when_withSuspendedStatus`
**Metrics:** LOC=5, PMC=4, DAT=False

```java
@Test
public void should_convertFromInternalProcessInstance_when_withSuspendedStatus() {
    ExecutionEntity internalProcessInstance = anInternalProcessInstance(APP_VERSION);

    internalProcessInstance.setSuspensionState(SuspensionState.SUSPENDED.getStateCode());

    ProcessInstance result = subject.from(internalProcessInstance);

    assertValidProcessInstanceResult(result);
    assertThat(result.getStatus()).isEqualTo(ProcessInstanceStatus.SUSPENDED);
}
```

#### 2. **Only DAT Smell Example**
**File:** `Activiti/AstBinaryTest.java`
**Method:** `testGetValue`
**Metrics:** LOC=2, PMC=2, DAT=True

```java
@Test
public void testGetValue() {
    assertEquals(
        Long.valueOf(2l),
        parseNode("${1+1}").getValue(bindings, null, null)
    );
    assertEquals(
        "2",
        parseNode("${1+1}").getValue(bindings, null, String.class)
    );
}
```

#### 3. **Both Eager and DAT Smells Example**
**File:** `Activiti/AstBinaryTest.java`
**Method:** `testOperators`
**Metrics:** LOC=8, PMC=8, DAT=True

```java
@Test
public void testOperators() {
    assertTrue(
        (Boolean) parseNode("${true and true}")
            .getValue(bindings, null, Boolean.class)
    );
    assertFalse(
        (Boolean) parseNode("${true and false}")
            .getValue(bindings, null, Boolean.class)
    );
    assertFalse(
        (Boolean) parseNode("${false and true}")
            .getValue(bindings, null, Boolean.class)
    );
    assertFalse(
        (Boolean) parseNode("${false and false}")
            .getValue(bindings, null, Boolean.class)
    );

    assertTrue(
        (Boolean) parseNode("${true or true}")
            .getValue(bindings, null, Boolean.class)
    );
    assertTrue(
        (Boolean) parseNode("${true or false}")
            .getValue(bindings, null, Boolean.class)
    );
    assertTrue(
        (Boolean) parseNode("${false or true}")
            .getValue(bindings, null, Boolean.class)
    );
    assertFalse(
        (Boolean) parseNode("${false or false}")
            .getValue(bindings, null, Boolean.class)
    );
}
```

### Verbose Smell Examples

#### 4. **Only Verbose Smell Example**

**File:** `Undertow/CompressionUtilsTest.java`
**Method:** `testPadding`
**Metrics:** LOC=14, PMC=0, DAT=False
PMC=0 => no method call made to production methods defined in repo

```java
  @Test
public void testPadding() throws Exception {
    String original = "This is a long message - This is a long message - This is a long message";
    byte[] compressed = new byte[1024];
    int nCompressed;

    compress.setInput(original.getBytes());
    nCompressed = compress.deflate(compressed, 0, compressed.length, Deflater.SYNC_FLUSH);

        /*
            Padding
         */
    byte[] padding = {0, 0, 0, (byte)0xff, (byte)0xff, 0, 0, 0, (byte)0xff, (byte)0xff, 0, 0, 0, (byte)0xff, (byte)0xff};
    int nPadding = padding.length;

    for (int i = 0; i < padding.length; i++) {
        compressed[nCompressed + i] = padding[i];
    }

    byte[] uncompressed = new byte[1024];
    int nUncompressed;

    decompress.setInput(compressed, 0, nCompressed + nPadding);
    nUncompressed = decompress.inflate(uncompressed);

    Assert.assertEquals(original, new String(uncompressed, 0, nUncompressed, "UTF-8"));
}
```

#### 5. **Only DAT Smell Example 
**File:** `commons-lang/DateUtilsFragmentTest.java`
**Method:** `testMinuteFragmentInLargerUnitWithCalendar`
**Metrics:** LOC=3, PMC=3, DAT=True

```java
@Test
public void testMinuteFragmentInLargerUnitWithCalendar() {
    assertEquals(0, DateUtils.getFragmentInMinutes(aCalendar, Calendar.MINUTE));
    assertEquals(0, DateUtils.getFragmentInHours(aCalendar, Calendar.MINUTE));
    assertEquals(0, DateUtils.getFragmentInDays(aCalendar, Calendar.MINUTE));
}
```

#### 6. **Both DAT and Verbose Smells Example**
**File:** `druid/OutputTypeTest.java`
**Method:** `testArrayFunctions`
**Metrics:** LOC=49, PMC=2, DAT=True

```java
  @Test
public void testArrayFunctions()
{
    assertOutputType("array(1, 2, 3)", inspector, ExpressionType.LONG_ARRAY);
    assertOutputType("array(1, 2, 3.0)", inspector, ExpressionType.DOUBLE_ARRAY);
    assertOutputType(
            "array(a, b)",
            inspector,
            ExpressionTypeFactory.getInstance().ofArray(ExpressionType.STRING_ARRAY)
    );

    assertOutputType("array_length(a)", inspector, ExpressionType.LONG);
    assertOutputType("array_length(b)", inspector, ExpressionType.LONG);
    assertOutputType("array_length(c)", inspector, ExpressionType.LONG);

    assertOutputType("string_to_array(x, ',')", inspector, ExpressionType.STRING_ARRAY);

    assertOutputType("array_to_string(a, ',')", inspector, ExpressionType.STRING);
    assertOutputType("array_to_string(b, ',')", inspector, ExpressionType.STRING);
    assertOutputType("array_to_string(c, ',')", inspector, ExpressionType.STRING);

    assertOutputType("array_offset(a, 1)", inspector, ExpressionType.STRING);
    assertOutputType("array_offset(b, 1)", inspector, ExpressionType.LONG);
    assertOutputType("array_offset(c, 1)", inspector, ExpressionType.DOUBLE);

    assertOutputType("array_ordinal(a, 1)", inspector, ExpressionType.STRING);
    assertOutputType("array_ordinal(b, 1)", inspector, ExpressionType.LONG);
    assertOutputType("array_ordinal(c, 1)", inspector, ExpressionType.DOUBLE);

    assertOutputType("array_offset_of(a, 'a')", inspector, ExpressionType.LONG);
    assertOutputType("array_offset_of(b, 1)", inspector, ExpressionType.LONG);
    assertOutputType("array_offset_of(c, 1.0)", inspector, ExpressionType.LONG);

    assertOutputType("array_ordinal_of(a, 'a')", inspector, ExpressionType.LONG);
    assertOutputType("array_ordinal_of(b, 1)", inspector, ExpressionType.LONG);
    assertOutputType("array_ordinal_of(c, 1.0)", inspector, ExpressionType.LONG);

    assertOutputType("array_append(x, x_)", inspector, ExpressionType.STRING_ARRAY);
    assertOutputType("array_append(a, x_)", inspector, ExpressionType.STRING_ARRAY);
    assertOutputType("array_append(y, y_)", inspector, ExpressionType.LONG_ARRAY);
    assertOutputType("array_append(b, y_)", inspector, ExpressionType.LONG_ARRAY);
    assertOutputType("array_append(z, z_)", inspector, ExpressionType.DOUBLE_ARRAY);
    assertOutputType("array_append(c, z_)", inspector, ExpressionType.DOUBLE_ARRAY);

    assertOutputType("array_concat(x, a)", inspector, ExpressionType.STRING_ARRAY);
    assertOutputType("array_concat(a, a)", inspector, ExpressionType.STRING_ARRAY);
    assertOutputType("array_concat(y, b)", inspector, ExpressionType.LONG_ARRAY);
    assertOutputType("array_concat(b, b)", inspector, ExpressionType.LONG_ARRAY);
    assertOutputType("array_concat(z, c)", inspector, ExpressionType.DOUBLE_ARRAY);
    assertOutputType("array_concat(c, c)", inspector, ExpressionType.DOUBLE_ARRAY);

    assertOutputType("array_contains(a, 'a')", inspector, ExpressionType.LONG);
    assertOutputType("array_contains(b, 1)", inspector, ExpressionType.LONG);
    assertOutputType("array_contains(c, 2.0)", inspector, ExpressionType.LONG);

    assertOutputType("array_overlap(a, a)", inspector, ExpressionType.LONG);
    assertOutputType("array_overlap(b, b)", inspector, ExpressionType.LONG);
    assertOutputType("array_overlap(c, c)", inspector, ExpressionType.LONG);

    assertOutputType("array_slice(a, 1, 2)", inspector, ExpressionType.STRING_ARRAY);
    assertOutputType("array_slice(b, 1, 2)", inspector, ExpressionType.LONG_ARRAY);
    assertOutputType("array_slice(c, 1, 2)", inspector, ExpressionType.DOUBLE_ARRAY);

    assertOutputType("array_prepend(x, a)", inspector, ExpressionType.STRING_ARRAY);
    assertOutputType("array_prepend(x, x_)", inspector, ExpressionType.STRING_ARRAY);
    assertOutputType("array_prepend(y, b)", inspector, ExpressionType.LONG_ARRAY);
    assertOutputType("array_prepend(y, y_)", inspector, ExpressionType.LONG_ARRAY);
    assertOutputType("array_prepend(z, c)", inspector, ExpressionType.DOUBLE_ARRAY);
    assertOutputType("array_prepend(z, z_)", inspector, ExpressionType.DOUBLE_ARRAY);
}
```
