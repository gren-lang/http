# HTTP

Make HTTP requests in Gren. Talk to servers.

## Examples

Here are some commands you might create to send HTTP requests with this package:

```gren
import Http
import Json.Decode as D

type Msg
  = GotBook (Result Http.Error String)
  | GotItems (Result Http.Error (Array String))

getBook : Cmd Msg
getBook =
  Http.get
    { url = "https://gren-lang.org/assets/public-opinion.txt"
    , expect = Http.expectString GotBook
    }

fetchItems : Cmd Msg
fetchItems =
  Http.post
    { url = "https://example.com/items.json"
    , body = Http.emptyBody
    , expect = Http.expectJson GotItems (D.array (D.field "name" D.string))
    }
```

