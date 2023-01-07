---
title: "Projects"
toc: true
draft: true
---

## KPEG

[{{< figure src="/img/kpeg.png" alt="KPEG logo" position="left" style="border-radius: 0;" caption="https://kpeg.io" captionPosition="center" captionStyle="color: black;" >}}](https://kpeg.io)

Kotlin PEG[^1] parser with Kotlin DSL[^2].

The project is inspired by the [pest parser](https://pest.rs/) and the [kotlin-peg-dsl project](https://github.com/mikaelhg/kotlin-peg-dsl).

All these projects use parsing expression grammars (or PEG) as input.
The main purpose of PEGs is to provide parsers convenient grammar to describe your language.

[^1]: Parsing Expression Grammar
[^2]: Domain Specific Language

> **[From Wikipedia](https://en.wikipedia.org/wiki/Parsing_expression_grammar)**:
> In computer science, a parsing expression grammar (PEG), is a type of analytic formal grammar, i.e. it describes a formal language in terms of a set of rules for recognizing strings in the language.

{{< code language="kotlin" title="Simple usage example" expand="Show" collapse="Hide" isCollapsed="false" >}}
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

println(evalExpr("+1 + 2 + -3 + +4 + 5")) // prints "9"
{{< /code >}}


## Mini Go

Link to github: https://github.com/AzimMuradov/mini-go

Mini Go (Golang) parser and interpreter written in Haskell.


## Mini Oracle

Link to github: https://github.com/AzimMuradov/mini-oracle

Mini-oracle can answer your questions. It's a full-stack machine-learning application that uses Hugging Face, Streamlit, Telegram Bot API, and Railway.