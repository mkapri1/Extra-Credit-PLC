# Extra-Credit-PLC
## **Specification Document**

### Keyword List
  |Keyword| Representation|
  |-------|-------|
  |IF| $|
  |ELSE| &|
  |BEGIN| #|
  |END| @|
  |Declaration| varie|

  | | |
  |--|--|
  |Addition| + |
  |Subraction| -|
  |Multiplication| *|
  |Division| /|
  |Modulus| %|
  |Left Paren| ( |
  |Right Paren| )|
  |End of Statement| ;|
  |Greater than| >|
  |Less than| < |
  |Greater than equal to| ~|
  |Less than equal to| ^ |
  |Equal| ==|
  |Not Equal| != |
  |Assignment| = |
  
  int_lit
  boolean -> Yes and No
  
### Grammar
  ````
  <program> --> `#`<stmt_list>`@`
  <stmt_list> --> { <stmt>`;`}
  <stmt> --> <if_stmt> | <while_loop> | <assignment> | <block> |  <declare> 
  <if_stmt> --> `$` `(`<bool_expr> `)` <stmt> [`&` <stmt>]
  <while_loop> --> `ROF` `(` <bool_expr> `)` <stmt>
  <assignment> --> `id` `=` <expr> `;`
  <block> --> `{`<stmt_list>`}`
  <declare> --> `varie` `id` `;`
  <expr> --> <term> {(`*`|`/`|`%`)} <term>
  <term> -->  <factor> {(`+`|`-`)} <factor>
  <factor> --> `id`| `int_lit`| `(`<expr>`)`

  <bool_expr> --> <rel> {(`!=`|`==`)} <rel>
  <rel> --> <bex> {(`<`|`>`|`~`|`^`)} <bex>
  <bex> --> <bterm> {(`*`|`/`|`%`)} <bterm>
  <bterm> --> <bfactor> {(`+`|`-`)} <bfactor>
  <bfactor> --> `id`|`int_lit`|`bool_lit`|`(`<bex>`)`

```` 

### Semantics
IF-ELSE:
````
 <if_stmt> -> $(<bool_expr>) <stmt> [ & <stmt>m ]
 
 M_if(if (bool_expr) <stmt>, s) -->
    
    if M_b(<bool_expr>, s) == error
      return error
    
    if M_b (<bool_expr>,s) 
       if M_stmt(<stmt>,s) == error
          return error
       return M_stmt(<stmt>,s)
       
 M_if($ (bool_expr) <stmt1>, & <stmt2>, s) -->
    
     if M_b(<bool_expr>, s) == error
      return error
     
     if M_b (<bool_expr>,s) 
       if M_stmt(<stmt1>,s) == error
          return error
       return M_stmt(<stmt1>,s)
       
     else
        if M_stmt(<stmt2>,s) == error
          return error
        return M_stmt(<stmt2>,s)
        
````

    
  
