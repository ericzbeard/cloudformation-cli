{% autoescape false %}
# {{ type_name }}
{% if schema.description %}

{{ schema.description }}
{% endif %}

## Activation

To activate a hook in your account, use the following JSON as the `Configuration` request parameter for [`SetTypeConfiguration`](https://docs.aws.amazon.com/AWSCloudFormation/latest/APIReference/API_SetTypeConfiguration.html) API request.

### Configuration

<pre>
{
    "CloudFormationConfiguration": {
        "<a href="https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/hooks-structure.html#hooks-hook-configuration" title="HookConfiguration">HookConfiguration</a>": {
            "<a href="https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/hooks-structure.html#hooks-targetstacks" title="TargetStacks">TargetStacks</a>":  <a href="#footnote-1">"ALL" | "NONE"</a>,
            "<a href="https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/hooks-structure.html#hooks-failuremode" title="FailureMode">FailureMode</a>": <a href="#footnote-1">"FAIL" | "WARN"</a> ,
            "<a href="https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/hooks-structure.html#hooks-properties" title="Properties">Properties</a>" : {
{% if schema.properties %}
{% for propname, prop in schema.properties.items() %}
{% if not prop.readonly %}
                "<a href="#{{ propname.lower() }}" title="{{ propname }}">{{ propname }}</a>" : <i>{{ prop.jsontype }}</i>{% if not loop.last %},{% endif %}

{% endif %}
{% endfor %}
{% endif %}
            }
        }
    }
}
</pre>
{% if schema.properties %}

## Properties

{% for propname, prop in schema.properties.items() %}
{% if not prop.readonly %}
#### {{ propname }}
{% if prop.description %}

{{ prop.description }}
{% endif %}

_Required_: {% if propname in schema.required %}Yes{% else %}No{% endif %}


_Type_: {{ prop.longformtype }}
{% if prop.allowedvalues %}

_Allowed Values_: {% for allowedvalue in prop.allowedvalues %}<code>{{ allowedvalue }}</code>{% if not loop.last %} | {% endif %}{% endfor %}

{% endif %}
{% if prop.minLength %}

_Minimum_: <code>{{ prop.minLength }}</code>
{% endif %}
{% if prop.maxLength %}

_Maximum_: <code>{{ prop.maxLength }}</code>
{% endif %}

{% endif %}
{% endfor %}
{% endif %}

---
<p id="footnote-1"><i> Please note that the enum values for <a href="https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/hooks-structure.html#hooks-targetstacks" title="TargetStacks">
TargetStacks</a> and <a href="https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/hooks-structure.html#hooks-failuremode" title="FailureMode">FailureMode</a>
might go out of date, please refer to their official documentation page for up-to-date values. </i></p>

{% endautoescape %}
