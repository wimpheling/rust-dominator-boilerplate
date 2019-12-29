Prepare app.rs
===

add a file app.rs inside src folder.
then copy the following into app.rs

```
use std::rc::Rc;
use lazy_static::lazy_static;
use dominator::{Dom, class, html};

pub struct App {
}

impl App {

    pub fn new() -> Rc<Self> {

        Rc::new(Self {
        })
    }

    pub fn render(app: Rc<Self>) -> Dom {
        
        lazy_static! {
            static ref ROOT_CLASS: String = class! {
                .style("overflow-x", "hidden")
                .style("color", "red")
            };
        }
        
        html!("div", {
            .class(&*ROOT_CLASS)
            .text("Hello World!")
        })
    }
}
```

## Test build

```
cargo web build
```
