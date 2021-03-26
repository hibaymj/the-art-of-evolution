openapi: 3.0.0
info:
  title: Martian Trail
  version: '0.1'
  description: |
    This is the API for the Martian Trail game. The API contract defines a very robust set of consistent resources and affordances with varied interaction patterns within a single API. The game is implemented using hypermedia to substantially simplify creating interfaces using the game core. If developers are unfamiliar with the use of hypermedia this API also includes several patterns which may be more familiar. These patterns require significantly more work to create a working client and have higher costs due to the unnecessary and substantial additional load they place on the game systems. Many factors contribute to this extraneous developmental and runtime load, but the primary cause is a self sustaining relationship between the following:
    * Exposing unnecessary __internal__ implementation details,values, methods,algorithms.
    * Insufficient or ambiguously __defined__, or inapprpriately scoped interfaces.
    
    Traditional solutions to this common mistake come from an incomplete understanding of the complex cause of the issue from a biased focus on _alleviating symptoms_ rather than __addressing causes__. These approaches almost invariably include introducing API versioning, assigning API design to implemention teams. This introduces the need to manage the lifecycle of these APIs both internally and with consumers. These changes significantly diminish incentives to design for general reusablity as teams are incentivized to design for specific known use cases. Lower quality design and lack of reusability is extremely detrimental on its own, and has the further undesirable effect of leading to further use of __symptom solutions__ like versioning. All of this is in the hope of making it easier for Consumer developers to make up for the poor design and implementation provided by the Producers.
    
    Consumer developers will find that the hypermedia driven REST will simplify their implementations considerably as they won't need to make up for these design issues and emulate internal game state to include stateful displays or contextual interactions within their client. For example, all __Orbital Bodies__ have the affordance (potential ability) to __Change Orbit__. In order determine if an __Orbital Body__ can __execute__ the __Change Orbit__ affordance a complex calculation is performed which looks at many factors including but not limited to: 
    * __Internal simulation implementation__ approximations and limits to effects such as gravity.
    * The existence of a propulsion system.
    * Sufficient fuel, power, reaction mass, medium, or field.
    * Any natural states which could induce a change in velocity.
    * The Body's __mass__.
    * And more where the properties and values are all subject to change without notice or guarantee.
    
    Generalizing the need outlined in the __Change Orbit__ example, the Consumer developer needs to know this substantial internal data and algorithm to answer a very simple question: "Can _this body_ change orbit? If yes, how?". Our REST interaction pattern uses hypermedia to answer both of these questions. The first is answered by the presence and absence of the affordance on the resource itself. We answer the latter question by defining specific, granular, and explicit messages which convey the information about the _consumer intent_. If the __Orbital Body__ in this case is a type of __Vehicle__ such as a __Spacecraft__ it may send a message like __Main-Engine-Burn__ containing details about orientation, duration, power levels, and desired change in velocity (delta-V). The service provider users hypermedia to inform the consumer that the __Orbital Body__ has the ability to __Change Orbit__ by sending it the __Main-Engine-Burn__ message.
    
    Instead of exposing this extreme level of internal coupling, we use hypermedia to avoid requiring consumer developers to resolve significant breaking changes at high frequencies when game designers modify an internal constant or add a new property to the calculation in certain circumstances. As you can see in the example above, the service Consumer is only providing the information they know which minimizes the difficulty of using this capability. This shelters consumers from the need to respond to, and even the awareness of, internal data and implementation changes.
    
    It is a significant investment for us to implement, maintain, and manage complex versioning lifecycles. Thus it is only undertaken when requested and necessary.
tags:
  - name: CRUD
    description:
      |
      This tag will show a basic view of CRUD operations on resources within the API. This may be the most fammiliar set of operations for use but will also require substantially more effort to successfully implement all but the simplest interactions.
  - name: REST
    description:
      |
      This tag will show operations which expose hypermedia driven self-descriptive affordances and state. The availability of these messages is not guaranteed at any point. They are entirely dependent on the resource internal context and state.
  - name: Vehicle
    description: This tag is for any Vehicle.
  - name: Orbital Body
    description: This tag is for any body in Orbit.
  - name: Planet
    description: This tag is for any Planet.
  - name: Moon
    description: This tag is for any natural large semi-spherical body orbiting a Planet.
  - name: Satellite
    description: This tag is for any artificial satellite of an orbital body.
  
paths:
  /vehicles:
    summary: Root Collection for Vehicles.
    description: >-
      This collection will provide the ability to search for specific vehicles
      in a variety of ways based on simple filtering or using message specific
      ways. Messages may offer specific affordances based on the response
      collection that do not exist on any individual vehicle or in any other
      context.
    post:
      summary: Create a new Vehicle or a complex message to the collection.
      description: >-
        This operation will CREATE a Vehicle and accept a complex message to the
        entire Vehicle collection. The complex message MAY use query parameters
        and or define complex SEARCH functionality which limits the scope from
        the entire collection. Over HTTP POST is unsafe and non-idempotent, thus
        it shouldn't be retried by consumers without first ensuring it hasn't
        executed or there are no side-effects to resource state as part of the
        message definition.
      operationId: vehicle-unsafe-non-idempotent-create-message
      responses:
        default:
          description: Default error sample response
      tags:
        - Vehicle
        - CRUD
        - Mesages
  /fleets:
    summary: Root Collection for Fleets.
    description: >-
      A fleet is a defined collection of Vehicles traveling together towards a
      common destination for mutual support. Fleets may be longstanding or
      temporary, structured or self-organizing, cyclical or one-way, and have
      simple or complex paths.
  /orbital-bodies:
    summary: Root Collection for Orbital Bodies.
    description: ''
  /orbits:
    summary: Root Collection for Orbits.
    description: >-
      Orbits are by definition a relationship between two bodies. Colloquially
      known as one body orbiting another. An orbit is actually a two body system
      where both bodies move around a common center of mass called a baricenter.
      This will have minimal impact if the difference in mass of the orbital
      bodies is large. However, this will become increasingly relevant when the
      difference in masses drops.
  /paths:
    summary: Root Collection for Paths.
    description: >-
      Paths are starting place with a sequence of one or more destinations. A
      starting place and destination can be defined as an Orbital-Body, a Fleet,
      or a specific Orbit.
  /orbital-maneuvers:
    summary: Root Collection for Orbital-Maneuvers.
    description: >-
      A sequence of one or more changes to orbital parameters such as
      orientation and delta-V (change to velocity) necessary to adjust an orbit.
      A static maneuver is a known quantity between two largely stationairy
      bodies like a Hohmann transfer from Earth to Earth L2 (Legrange 2). A
      dynamic maneuver is a definition of changes to orbit without a guaranteed
      destination.

