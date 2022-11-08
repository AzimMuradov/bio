---
title: "Projects"
draft: true
---

## KPEG

Link to website - https://kpeg.io

Kotlin PEG[^1] parser with Kotlin DSL[^2]

[^1]: Parsing Expression Grammar
[^2]: Domain Specific Language

> **[From Wikipedia](https://en.wikipedia.org/wiki/Parsing_expression_grammar)**:
> In computer science, a parsing expression grammar (PEG), is a type of analytic formal grammar, i.e. it describes a formal language in terms of a set of rules for recognizing strings in the language.

{{< code language="kotlin" title="Simple usage example" id="1" expand="Show" collapse="Hide" isCollapsed="false" >}}
val num = Symbol.rule<Int>(name = "Num", ignoreWS = false) {
    seq {
        val sign = +char('+', '-').orDefault('+')
        val digits = +DIGIT.oneOrMore().joinToString()

        value { (sign.get + digits.get).toInt() }
    }
}

val sum = Symbol.rule<Int>(name = "Sum") {
    num.list(separator = char('+'), min = 1u).mapPe { it.sum() }
}


fun evalExpr(expression: String) =
    PegParser.parse(symbol = sum.value(), expression).getOrElse { null }

val results = listOf(
    evalExpr("1"),                         // 1
    evalExpr("+1"),                        // 1
    evalExpr("+ 1"),                       // null
    evalExpr("+1 +"),                      // null
    evalExpr("-17"),                       // -17
    evalExpr("-1 7"),                      // null
    evalExpr("1+2+3+4+5"),                 // 15
    evalExpr("1 + +2 + -3 + +4 + 5"),      // 9
    evalExpr("definitely not expression"), // null
    evalExpr(""),                          // null
)

for (res in results) {
    println(res)
}
{{< /code >}}


## Mini Go

Link to github: https://github.com/AzimMuradov/fp2022-haskell/tree/mini-go/MiniGo

`TODO : Work In Progress`


## SMT Solver

`TODO : Work In Progress`
