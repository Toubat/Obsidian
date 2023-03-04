1. 5, no, "hi".
2. Environment
```
{x -> 3}
{x -> 3, f -> <y -> x + y, {x -> 3}>}
{x -> 5, f -> <y -> x + y, {x -> 3}>}
{x -> 5, f -> <y -> x + y, {x -> 3}>, z -> 5}
{x -> "hi", f -> <y -> x + y, {x -> 3}>, z -> 5}
```

```
Eval(f 2, {x -> 5, f -> <y -> x + y, {x -> 3}>})
=> Eval(f Eval(2, {x -> 5, f -> <y -> x + y, {x -> 3}>}, {x -> 5, f -> <y -> x + y, {x -> 3}>})
=> Eval(f (Val 2), {x -> 5, f -> <y -> x + y, {x -> 3}>})
=> Eval(Eval(f, {x -> 5, f -> <y -> x + y, {x -> 3}>}) (Val 2), {x -> 5, f -> <y -> x + y, {x -> 3}>})
=> Eval((Val <y -> x + y, {x -> 3}>) (Val 2), {x -> 5, f -> <y -> x + y, {x -> 3}>})
=> Eval(x + y, {x -> 3, y -> 2})
=> Eval(x + Eval(y, {x -> 3, y -> 2}), {x -> 3, y -> 2})
=> Eval(x + Val 2, {x -> 3, y -> 2})
=> Eval(Eval(x, {x -> 3, y -> 2}) + Val 2, {x -> 3, y -> 2})
=> Eval(Val 3 + Val 2, {x -> 3, y -> 2})
=> Val 5
```

3. 
	a. 
		print: "ba"
		return: 6
	b. 
		print: "ab"
		return: 6
	c. 
		print: "ab"
		return: 6

4. 
	a. loop1 cause stack overflow, loop2 runs forever.
	b. loop1 call recursive function first, the last operation of loop1 is not recursive call; loop2 call recursive function last.
	c. loop1: recursive, forward recursive; loop2: recursive, forward recursive, tail-recursive.

5. code below
```ocaml
let rec pair_up f list = match list 
	with [] -> []
	| x :: xs -> (x, f x) :: pair_up f xs;;

val pair_up: (a' -> b') -> a' list -> (a' * b') list
```

a. `[(6, 9); (4, 7); (1, 4)]`
b. `[("John", "Hi, John"); ("Mary", "Hi, Mary"); ("Dana", "Hi, Dana")]` *Type Error*
c. `float list -> (float * float) list`

6. code below
```ocaml
let rec palindrome list = match list 
	with [] -> ()
	| x :: xs -> print_string x; palindrome xs; print_string x;;

```

```ocaml
let rec pal list = List.fold_right (fun x -> fun pm -> fun () -> print_string x; pm (); print_string x) list (fun () -> ()) ();; 

let rec pal list = List.fold_left (fun pm -> fun x -> print_string x; (fun () -> print_string x; pm ())) (fun () -> ()) list ();;
```

7. code below
```ocaml
let concat list = List.fold_right (fun a -> fun b -> a @ b) list [];;
```

8. code below
	a.
```ocaml
let rec list_print list = match list
	with [] -> ()
	| x :: xs -> print_string x; list_print xs;;
```
	b. 
```ocaml
let list_print list = List.fold_left (fun x -> fun y -> print_string y) () list
```