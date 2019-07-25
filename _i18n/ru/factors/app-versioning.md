**Версия и номер билда используются вместе что бы идентифицировать конкретное приложение в аппсторе:**

- Номер версии (`CFBundleShortVersionString`) - показан как `Version` в Xcode, так же называется маркетной версию: Версия которая видна для пользователя, она должна быть поднята для каждого публичного релиза
- Номер билда (`CFBundleVersion`) - показан как `Build` в Xcode: нарастающие число

В сегодняшней разработки под iOS нет причин, по которым вы должны вручную менять эти цифры. Вместо этого вам нужна надежная и автоматизированная система, обеспечивающая актуальность версий.

Xcode имеет встроенный иснтрумент под названием `agvtool`. ([more details](https://developer.apple.com/library/content/qa/qa1827/_index.html))

После включение `Versioning System` для вашего Xcode проекта, можно использовать следующие команды:

```sh
# Обновить номер версии (CFBundleShortVersionString)
agvtool new-marketing-version 2.0

# Обновить номер сборки (CFBundleVersion) до следующего
agvtool next-version -all
```

Если вы пользуйтесь инструментом развертывания под названием [fastlane](https://fastlane.tools) можете использовать [increment_version_number](https://docs.fastlane.tools/actions/increment_version_number/) и [increment_build_number](https://docs.fastlane.tools/actions/increment_build_number/) для автоматизирования поднятий версий во время развертывания.

Пример `Fastfile`:

```ruby
lane :beta do
  increment_build_number
  build_ios_app
  testflight
end
```
