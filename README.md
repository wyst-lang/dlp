# Dynamic Library Protocol

## Structure
- `REQUEST` -> `[<id>, <fn_name>, <params>]`
- `RESPONSE` -> `[<id>, <param>]`

## Types and Values
- `is_fn` -> `bool`
- `param` -> `[<is_fn>, <JsonValue | fn_name>]`
- `id` -> `int`
- `fn_name` -> `string`
- `params` -> `array[param]`

## Example 1
- `RUN` -> `[23225, "0x2323834", [[false, 1], [false, 1]]]`
- `DLL` -> `[23225, [false, 2]]`

### Explanation
We call a function stored in a map (0x2323834), and we pass 2 parameters which both are integers (1, 1) and the function inside the dll returns a sum of the parameters (in this case 2). the response has the same id as the request because it's the output of that request

## Example 2
- `RUN` -> `[8664, "0x4573252", [[true, "0x2692626"]]`
- `DLL` -> `[23225, "0x2692626", [[false, 1], [false, 1]]]`
- `RUN` -> `[23225, "0x2692626", [false, 2]]`
- `DLL` -> `[8664, [false, 2]]`


### Explanation
We call a function stored in a map (0x4573252), and we pass 1 parameter that is a function which is inside the runtime itself (0x2692626), And the dll tells the runtime to run that function and the runtime sends the output of that call (sum), and the dll responds wit the output of the call
