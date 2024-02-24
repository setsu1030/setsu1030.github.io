+++
title = 'Goの「no new variables on left side of :=」について'
date = 2024-02-24T20:21:48+09:00
draft = false
tags = ['golang']
categories = ['備忘録']
+++
ん？と思うところがあったのでメモ。
### エラーにならないパターン
左辺の変数名が異なる場合、エラーにならない  
`b, err` と `c, err`
{{< code lang="go" title="main.go" >}}
func main() {
	var a A = A{}
	b, err := a.getB()
	if err != nil {
		log.Fatalln("Error")
	}
	c, err := a.getC() // エラーにならない
	if err != nil {
		log.Fatalln("Error")
	}
	log.Println(b, c)
}
{{< /code >}}
`b, err` と `b2, err`
{{< code lang="go" title="main.go" >}}
func main() {
	var a A = A{}
	b, err := a.getB()
	if err != nil {
		log.Fatalln("Error")
	}
	b2, err := a.getB() // エラーにならない
	if err != nil {
		log.Fatalln("Error")
	}
	log.Println(b, b2)
}
{{< /code >}}
* * *
### エラーになるパターン
左辺の変数名が同じ場合、エラーになる  
`b, err` と `b, err`
{{< code lang="go" title="main.go" >}}
func main() {
	var a A = A{}
	b, err := a.getB()
	if err != nil {
		log.Fatalln("Error")
	}
	b, err := a.getB() // no new variables on left side of :=
	if err != nil {
		log.Fatalln("Error")
	}
	log.Println(b)
}
{{< /code >}}
メソッドの戻り値がerrorのみの場合、エラーになる  
`b, err` と `err`
{{< code lang="go" title="main.go" >}}
func main() {
	var a A = A{}
	b, err := a.getB()
	if err != nil {
		log.Fatalln("Error")
	}
	err := a.getError() // no new variables on left side of :=
	if err != nil {
		log.Fatalln("Error")
	}
	log.Println(b)
}
{{< /code >}}
* * *
### メソッドの戻り値がerrorのみでもエラーにならないパターン
簡易文を設定したif文の場合、エラーにならない。  
（ `err` がif文のブロックの変数となるため）
{{< code lang="go" title="main.go" >}}
func main() {
	var a A = A{}
	b, err := a.getB()
	if err != nil {
		log.Fatalln("Error")
	}
	if err := a.getError(); err != nil { // エラーにならない
		log.Fatalln("Error")
	}
	log.Println(b)
}
{{< /code >}}
