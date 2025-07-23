
    {% for test in node.tests if config.testsEnabled %}
        {% if test.runOrder == 'Before' %}
            {{ test_stage(test.name, test.continueOnFailure) }}
            {{ test.templateString }}
        {% endif %}
    {% endfor %}

{% if node.materializationType == 'table' %}
	{% if config.preSQL %}
		{{ stage('Pre-SQL') }}
		{{ config.preSQL }}
	{% endif %}
	
	
	
		{% if config.truncateBefore %}
	
			{{ stage('Truncate Stage Table') }}
			TRUNCATE IF EXISTS {{ ref_no_link(node.location.name, node.name) }}
	
		{% endif %}
	
	
		{% if config.insertStrategy in ['UNION', 'UNION ALL'] %}
			{{ stage( config.insertStrategy + ' Sources' | string ) }}
			INSERT INTO {{ ref_no_link(node.location.name, node.name) }}
				(
					{% for col in columns %}
						"{{ col.name }}"
						{%- if not loop.last -%},{% endif %}
					{% endfor %}
				)
		{% endif %}
	
	
		{% for source in sources %}
	
			{% if config.insertStrategy == 'INSERT' %}
				{{ stage('Insert ' + source.name | string ) }}
	
				INSERT INTO {{ ref_no_link(node.location.name, node.name) }}
				(
					{% for col in source.columns %}
						"{{ col.name }}"
						{%- if not loop.last -%},{% endif %}
					{% endfor %}
				)
			{% endif %}
	
			SELECT
			{% for col in source.columns %}
                {{ get_source_transform(col) }} AS "{{ col.name }}"
				{%- if not loop.last -%}, {% endif %}
			{% endfor %}
	
			{{ source.join }}
	
			{% if config.insertStrategy in ['UNION', 'UNION ALL'] and not loop.last %}
				{{config.insertStrategy}}
			{% endif %}
	
		{% endfor %}
	
	{% if config.postSQL %}
		{{ stage('Post-SQL') }}
		{{ config.postSQL }}
	{% endif %}
{% endif %}

{% if config.testsEnabled %}
	{% for test in node.tests %}
		{% if test.runOrder == 'After' %}
			{{ test_stage(test.name, test.continueOnFailure) }}
			{{ test.templateString }}
        {% endif %}
	{% endfor %}

	{% for column in columns %}
		{% for test in column.tests %}
			{{ test_stage(column.name + ": " + test.name) }}
			{{ test.templateString }}
		{% endfor %}
	{% endfor %}
{% endif %}
