[//]: # ([![Build Status]&#40;https://travis-ci.com/Teamwork/tnef.svg?branch=master&#41;]&#40;https://travis-ci.com/Teamwork/tnef&#41;)

[//]: # ([![codecov]&#40;https://codecov.io/gh/Teamwork/tnef/branch/master/graph/badge.svg&#41;]&#40;https://codecov.io/gh/Teamwork/tnef&#41;)

[//]: # ([![GoDoc]&#40;https://godoc.org/github.com/Teamwork/tnef?status.svg&#41;]&#40;https://godoc.org/github.com/Teamwork/tnef&#41;)

With this library you can extract the body and attachments from Transport
Neutral Encapsulation Format (TNEF) files.

This repository is a fork of https://github.com/Teamwork/tnef with fixes for attachment and integrates various other fixes from other forks.

This is based on https://github.com/koodaamo/tnefparse and
http://www.freeutils.net/source/jtnef/.

## Example usage

```go
package main
import (
	"io/ioutil"
	"os"

	"github.com/samarec1812/mail-tnef"
)

func main() {
	t, err := tnef.DecodeFile("./winmail.dat")
	if err != nil {
		return
	}
	wd, _ := os.Getwd()
	for _, a := range t.Attachments {
		os.WriteFile(wd+"/"+a.Title, a.Data, 0777)
	}
	os.WriteFile(wd+"/bodyHTML.html", t.BodyHTML, 0777)
	os.WriteFile(wd+"/bodyPlain.html", t.Body, 0777)
}
```
