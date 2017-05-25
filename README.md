# Query Param Group

> Combined query parameters for Rocket

## Usage

```rust
extern crate query_param_group;
use query_param_group::{NamedFields, QueryParamGroup};

#[derive(FromForm)]
struct LimitParam {
  limit: i32,
}
impl NamedFields for LimitParam {
  const FIELDS: &'static [&'static str] = &["limit"];
}

#[derive(FromForm)]
struct UserNameParam {
  usercount: i32,
}
impl NamedFields for UserNameParam {
  const FIELDS: &'static [&'static str] = &["usercount"];
}

#[get("/users?<query_params>")]
fn get_users(
  query_params: QueryParamGroup<(LimitParam, UserNameParam)>
) -> i32 {
  let qp = query_params.get();
  // now, for some nonsensical code!
  qp.0.limit + qp.1.usercount
}
```

## Thanks

[Sergio Benitez](github.com/SergioBenitez) helped start me off on the right path!