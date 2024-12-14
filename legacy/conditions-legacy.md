# Conditions (Legacy)

## None

No condition.

```yaml
- 'none'
```

## World

Player must be in those worlds.

Use `;;` to separate each world.

<pre class="language-yaml"><code class="lang-yaml"><strong>- 'world: World1;;World2'
</strong></code></pre>

## Permission

Player must have all those permissions.

**Remember that OP players will always have all permissions unless plugin set it not by default, so if you want to test this condition, you have to deop yourself.**

Use `;;` to separate each permissions.

<pre class="language-yaml"><code class="lang-yaml"><strong>- 'permission: permission.1;;permission.2'
</strong></code></pre>

## Placeholder

Player must be meet the placeholder condition. It consists of three parts, separated by `;;`. The format is `<Placeholder>;;<Conditional Character>;;<Value>`.

Conditional character can be set to:

* \>=
* <=
* \>
* <
* \== (String)
* \= (Number)
* != (Number or string)
* !\*= (Number or string) Not contains.
* \*= (String) Contains, for example, str \*= string is true, but example \*= ple is false.

```yaml
- 'placeholder: %player_points%;;>=;;200'
```
