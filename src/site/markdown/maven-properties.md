keywords: velocity
description: ${project.name} allows writers to reference Maven pom.xml properties.

# Maven properties (`${property}`)

<!-- MACRO{toc|fromDepth=1|toDepth=2|id=toc} -->

All properties defined in `pom.xml` can be referenced in the Markdown source documents (and others) using the `${propertyName}` syntax, and will be replaced with their corresponding value in the resulting HTML.

> **Note**
>
> This is different from the default behavior of Maven Site and most skins. An extra-processing is performed with the *Sentry Maven Skin* to allow this feature.

Similarly, all properties defined in `site/site.xml` under the `<custom>` tag can also be referenced with the `$decoration.getCustomValue("propertyName")` syntax.

## Properties in `pom.xml`

Example of a `pom.xml`:

```xml
<project>
  ...
  <properties>
    <productShortname>MetricsHub</productShortname>
    <serviceUrl>https://metricshub.com/api</serviceUrl>
    ...
  </properties>
```

In the source documents (`src/site/markdown/*.md`, or others), you can use `$productShortname` and `$serviceUrl`, which will be replaced with their corresponding value in the produced HTML:

```md
**$productShortname** allows administrators to setup the monitoring of any application through an [API]($serviceUrl)...
```

This will produce the below result:

> **MetricsHub** allows administrators to setup the monitoring of any application through an [API](https://metricshub.com/api)...

## Properties in `src/site/site.xml`

Same principle goes with `src/site/site.xml`, with properties listed under `<custom>`:

```xml
<project name="My Documentation">

  ...

  <custom>
    <productShortname>MetricsHub</productShortname>
    <serviceUrl>https://metricshub.com/api</serviceUrl>
    ...
  </custom>

```

In the source documents (`src/site/markdown/*.md`, or others), you can use `$decoration.getCustomValue("productShortName")` and `$decoration.getCustomValue("serviceUrl")`, which will be replaced with with their corresponding value:

```md
**$decoration.getCustomValue("productShortName")** allows administrators to setup the monitoring of any application through an [API]($decoration.getCustomValue("serviceUrl"))...
```

This will produce the below result:

> **MetricsHub** allows administrators to setup the monitoring of any application through an [API](https://metricshub.com/api)...

> **Note**
>
> The syntax to reference values in `pom.xml` looks nicer and easier than the syntax for `src/site/site.xml`. However, it's the latter method that is recommended so that documentation information remains in `src/site/site.xml` rather than spread across several configuration files.
