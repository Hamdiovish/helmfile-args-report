# Context

This is a simple helm chart containing one config-map with two values "first_name" and "last_name".
We want to update these values using helmfile using the steps below. 

# Steps
1. Run helmfile for the 1st time:
>helmfile -f helmfile.yaml sync --values staging-values-01.yaml

As expected, "first-name" will be "spring" and "last_name" will be "boot".

2. ReRun helmfile with different values:

>helmfile -f helmfile.yaml sync --values staging-values-02.yaml --args "--reuse-values"

Let say we want to update only the "last_name" and we omitted "first_name" from the values.yaml since we expect that it will remain the same:

What happens after running the command is that the "last_name" is updated, but the "first_name" which is removed in the "staging-values-02.yaml" has been restored to the default value of the chart instead of remaining at the previous value.

So instead of having "first_name: spring" and "last_name: mvc", we got "fist_name: lorem" and "last_name: mvc"

We observed the same behaviour with "helmfile sync" and "helmfile update".