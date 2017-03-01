# My first pattern book

## Programming: Mapping data

To transform a list of length x to another list of length x.

This is a common pattern:

```
def investor_profiles
  profiles = []
  Investor.all.each do |investor|
    profiles << InvestorProfile.new(investor)
  end
  profiles
end
```
Which can be rewritten as:
```
def investor_profiles
  Investor.all.map do |investor|
    InvestorProfile.new(investor)
  end
end
```

## Programming: Redundant return logic

When returning the result of a condition check, sometimes we write this:

```
def valid?(account)
  return false if account.email.blank? || account.password.blank?
  true
end
```

or

```
def valid?(account)
  if account.email.present? && account.password.present?
    true
  else
    false
  end
end
```

where it can be rewritten as

```
def valid?(account)
  account.email.present? && account.password.present?
end
```

The change between `account.email.blank? || account.password.blank?` and `account.email.present? && account.password.present?` can be explained by a simple law (De Morgan's laws): `(A || B) == !(!A && !B)` or `(A && B) == !(!A || !B)` which roughly translates into something like: `(objectA.present? || objectB.present?) == !(objectA.blank? && objectB.blank?)`



