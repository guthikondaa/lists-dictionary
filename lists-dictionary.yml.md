# YAML Syntax for Ansible

* http://docs.ansible.com/ansible/YAMLSyntax.html
* http://docs.ansible.com/

## Lists

* Option 1:

```yaml
fruits:
    - Apple
    - Orange
    - Strawberry
    - Mango
```

* In valid JSON:

```json
{"fruits":["Apple","Orange","Strawberry","Mango"]}
```

* Option 2:

```yaml
- debug: msg='fruit name {{item}}'
  with_items: fruits
- debug: msg='fruit name {{item}}'
  with_items: fruits
```

* In valid JSON:

```json
[{"debug":"msg='fruit name {{item}}'","with_items":"fruits"},{"debug":"msg='fruit name {{item}}'","with_items":"fruits"}]
```

## Dictionary

* Option 1:

```yaml
instructions:
  - name: server1
    subject: pepito
  - name: server2
    subject: juanito
```

* In valid JSON:

```json
{"instructions":[{"name":"server1","subject":"pepito"},{"name":"server2","subject":"juanito"}]}
```

* Usage:

```yaml
- command: path={{ item.name }} mode={{ item.subject }}
  with_items: instructions
```

* Option 2:

```yaml
- martin:
    name: Martin D'vloper
    job: Developer
    skill: Elite
- john:
    name: John D'vloper
    job: PM
    skill: Elite
```

* In valid JSON:

```json
[{"martin":{"name":"Martin D'vloper","job":"Developer","skill":"Elite"}},{"john":{"name":"John D'vloper","job":"PM","skill":"Elite"}}]
```

* Option 3:

```yaml
employees:
  -  martin: {name: Martin D'vloper, job: Developer, skill: Elite}
  -  john: {name: John D'vloper, job: PM, skill: Elite}
```

## Dictionary with subitems

```yaml
- prod_list:
  - prod_name: "unknown product"
      prod_serial: "123456"
      prod_location: /opt/product1"
  - prod_name: "popular product"
      prod_serial: "987654"
      prod_location: /opt/product2"
```

* Usage:

```yaml
- debug: msg="product name {{item.prod_name}} serial {{item.prod_serial}} location {{item.prod_location}}"
  with_items: prod_list
```
