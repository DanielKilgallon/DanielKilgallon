```Rust
fn main() {
  let danny = SoftwareDeveloper {
    pronouns: String::from("he/him"),
    username: String::from("DanielKilgallon"),
    email: String::from("danielkilgallon2@gmail.com"),
    languages: [
      String::from("Rust"),
      String::from("Java"),
      String::from("Javascript/Typescript"),
    ],
    goal: String::from("To contribute to open source!"),
  };
}

struct SoftwareDeveloper {
  pronouns:  String,
  username:  String,
  email:     String,
  languages:[String; 3],
  goal:      String,
}
```

---

[![Github stats](https://github.com/danielkilgallon/github-stats/blob/master/generated/overview.svg)](https://github.com/DanielKilgallon/DanielKilgallon)
