{{ resource }}
=========================================

**{{ resource }}** is one of {{ resource.domain.num_services() }} services in the {{ resource.domain }} domain.


{% if resource.state_chart.is_populated() %}
State Chart
-----------


.. blockdiag::

   blockdiag {{ resource }} {
      orientation=portrait;

      // states{% for state in resource.state_chart.get_concrete_states() %}
      {{ state }} [shape=roundedbox];{% endfor %}

      // mutations{% for t in resource.state_chart.get_internal_transitions() %}
      {{ t.from_state }} -> {{ t.to_state }}{% if t.name %} [label={{ t.name }}]{% endif %};{% endfor %}

      // constructors{% if resource.state_chart.has_constructor_transitions() %}
      genesis_state [shape=beginpoint, label=""];
      {% for t in resource.state_chart.get_constructor_transitions() %}
      genesis_state -> {{ t.to_state }}{% if t.name %} [label={{ t.name }}]{% endif %};{% endfor %}{% endif %}
      
      // destructors{% if resource.state_chart.has_destructor_transitions() %}
      terminal_state [shape=endpoint, label=""];
      {% for t in resource.state_chart.get_destructor_transitions() %}
      {{ t.from_state }} -> terminal_state{% if t.name %} [label={{ t.name }}]{% endif %};{% endfor %}{% endif %}
   }
{% endif %}

Entity / Relationship Diagram
-----------------------------

TODO: insert ERD

