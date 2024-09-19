# go-tg-auth

This Go module validates Telegram authorization data by checking the hash of the provided authorization data against a calculated hash using the Telegram bot token.
You can find a detailed reference for the validation in the [official Telegram documentation](https://core.telegram.org/widgets/login#checking-authorization).

## Installation

```bash
go get github.com/mistermelphin/go-tg-auth
```

## Usage

Below is an example of how to use the `tg-auth` module to validate Telegram authorization data.

```go
package main

import (
    "fmt"
    "log"
    "github.com/mistermelphin/go-tg-auth"
)

const botToken = "123:4567890"

func main() {
    base64encoded := []byte("content")
    authData, err := tg_auth.ParseAuthDataBase64(base64encoded)
    if err != nil {
        log.Fatalf("Error parsing auth data: %v", err)
    }

    if err := authData.Validate([]byte(botToken)); err != nil {
        log.Fatalf("Validation failed: %v", err)
    }

    fmt.Printf("Validated user %d (@%s) logged in", *authData.Id, *authData.Username)
}
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
