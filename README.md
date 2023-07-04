# IPLD Inline Link Specification v0.1.0
-- FIXME transclusion?

## Editors

* [Brooklyn Zelenka], [Fission]

## Authors

* [Brooklyn Zelenka], [Fission]
* [Irakli Gozalishvili], [Protocol Labs]
* [Philipp Krüger], [Fission]

## Language

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119].

## Dependencies

* [IPLD]

# 0 Abstract

Spanning DAG is a container for IPLD which exists somewhere between an unpacked representation and a [CAR file]. It includes many quality of life features including inlined linked DAGs and inherited encoding.

# 1 Introduction

# 1.1 Motivation

[IPLD] is a format for describing Merkle DAGs with semantics similar to CBOR plus hash linking to other IPLD. The standard 

It is often desirable to print IPLD with links inlined.

There's a difference in hashing between having data inline versus inserting a link. This helps. BUt also when you do this normally, you have to pick an encoding: you can just inherit.

Versus identity CIDs.

## 1.2 Design

[IPLD] is a deterministic encoding scheme for data expressed in [common types][IPLD Data Model] plus content addressed links. The links are typically tabled.

Versus CARs which are tables

Combinng the two

# 2 IPLD Schema

``` ipldsch
type InlineLink struct {
  cid nullable Link (implicit Null)
  dag          Any
}

type InlineWrapper struct {
  inline InlineLink (rename "/")
}
```

Not just the encoding because 

Note! Cannot just hash to check anymore. You need to actually unpack the container.

optionally wrap the entire thig in a Wraper.

Spanning trees

Similar to `{"/": {"bytes": ...}}`

## 2.1 

## Explicit 

``` js
{
  "/": {
    "cid": "bafyreig6gfqs6rm3w64hbffgcste5iugr3imvvum5yrouhuy5qgdjdcdiu", // Encoded as DAG-CBOR
    "dag": {
      "day": 29,
      "month": 9
    }
  }
}
```

``` ipldsch
{
  "age": 3,
  "name": "Smokey",
  "owner": {
    "/": {
      "cid": null, // Inherits encoding from container
      "dag": {
        "name": "Katie",
        "species": "human"
      }
    }
  },
  "species": "cat",
  ""
}
```

# 4 Canonicalization

Left-heavy spanning tree




<!-- TODOS -->


```
-- FIXME use a feature table instead?
type SpanningCapsule struct {
  capsule Any (rename "ipld/spanning/v0.1")
  canon   Bool (implicit false)
}

type FeatureTable struct {
   
}

type Capsule struct {
  head FeatureTable (implicit {})
  data Any (rename "ipld/ext/v0.1")
}
```

<!-- Links -->

[Brooklyn Zelenka]: https://github.com/expede 
[Fission]: https://fission.codes
[Irakli Gozalishvili]: https://github.com/Gozala
[Philipp Krüger]: https://github.com/matheus23
