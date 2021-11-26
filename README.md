# circleci-with-t

[CircleCI](http://circleci.com) without code but only config.yml. This project test the web pages return `200` HTTP code.

**No code! Only config.yml!**

These commands that comes true:

* **t** - https://github.com/yusukebe/t
* **rj** - https://github.com/yusukebe/rj
* **jq** - https://github.com/stedolan/jq

## Test command

```
$ rj https://example.com/ | jq .code | t 200
```

## Example of config.yml

```yaml
version: 2.1
jobs:
  test:
    parameters:
      url:
        type: string
    docker:
      - image: cimg/go:1.17.3
    steps:
      - run:
          command: go install github.com/yusukebe/rj/cmd/rj@latest
      - run:
          command: go install github.com/yusukebe/t/cmd/t@latest
      - run:
          name: Test << parameters.url >>
          command: rj <<parameters.url>> | jq '.code' | t 200
workflows:
  test_workflow:
    jobs:
      - test:
          url: https://example.com/
          url: https://yusukebe.com/
```

## Screenshots

![Screenshots](https://user-images.githubusercontent.com/10682/143546939-f4ee6537-1170-48eb-a711-d71856323859.png)

## Author

Yusuke Wada <https://github.com/yusukebe>

## License

MIT