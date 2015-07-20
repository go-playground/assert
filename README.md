Package assert
==============

Package assert is a Basic Assertion library used along side native go testing

Usage and documentation
------

##### Example:
```go
package whatever

import (
	"errors"
	"testing"
)

func AssertCustomErrorHandler(t *testing.T, errs map[string]string, key, expected string) {
	val, ok := errs[key]

	// using EqualSkip and NotEqualSkip as building blocks for my custom Assert function
	EqualSkip(t, 2, ok, true)
	NotEqualSkip(t, 2, val, nil)
	EqualSkip(t, 2, val, expected)
}

func TestEqual(t *testing.T) {

	// error comes from your package/library
	err := errors.New("my error")
	NotEqual(t, err, nil)
	Equal(t, err.Error(), "my error")

	err = nil
	Equal(t, err, nil)

	fn := func() {
		panic("omg omg omg!")
	}

	PanicMatches(t, func() { fn() }, "omg omg omg!")
	PanicMatches(t, func() { panic("omg omg omg!") }, "omg omg omg!")

	// errs would have come from your package/library
	errs := map[string]string{}
	errs["Name"] = "User Name Invalid"
	errs["Email"] = "User Email Invalid"

	AssertCustomErrorHandler(t, errs, "Name", "User Name Invalid")
	AssertCustomErrorHandler(t, errs, "Email", "User Email Invalid")
}
```

How to Contribute
------

There will always be a development branch for each version i.e. `v1-development`. In order to contribute, 
please make your pull requests against those branches.

If the changes being proposed or requested are breaking changes, please create an issue, for discussion 
or create a pull request against the highest development branch for example this package has a 
v1 and v1-development branch however, there will also be a v2-development brach even though v2 doesn't exist yet.

I strongly encourage everyone whom creates a usefull custom assertion function to contribute them and
help make this package even better.

License
------
Distributed under MIT License, please see license file in code for more details.