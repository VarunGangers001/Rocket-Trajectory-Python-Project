- Thrust = F = $\dot{m}$ $V_e$ + ($p_e$ - $p_0$) $A_e$ 
- The amount of thrust depends on the mass flow rate through the engine, the exit velocity of the exhaust, and the pressure at the nozzle exit.
- The smallest cross-sectional area of the nozzle is called the **throat**. 
- $V_e$ = exit velocity, $A_e$ = area ratio of throat to exit, $p_e$ = exit pressure
- In the thrust eq, notice there is no free stream velocity term because no external air is brought on board.
	- Oxidizer carried onboard rocket, so rocket can generate thrust in in a vacuum where there is no other source of oxygen.
- On a rocket, **thrust** is used in opposition to weight. On many rockets, lift is used to stabilize and control the direction of flight.
- The **drag** of a rocket is usually much greater than the lift.
- A rocket gets lighter during flight, due to the expulsion of fuel, but while thrust stays the same this leads to an increase in acceleration
- The gravitational force, F, between two particles depends on their masses, $m_1$ & $m_2$, the distance between them, d, an a universal gravitational constant, G.
- F = $\frac{G m_1 m_2}{d^2}$ 
- **Lift** and **drag** depend on shape of the rocket, its size, and its velocity. They also depend on the properties of the atmosphere.
- Drag decreases as a rocket gains altitude because the Earth's atmospheric density drops exponentially the higher the rocket goes.

**Governing Equation:** 
The trajectory of a rocket is Newton's Second Law of Motion for variable mass, giving acceleration at a given instant during the rocket's flight

a = $\frac{T(t) - m(t)g - D(v,h)}{m(t)}$     (1)

Newton's second law says force equals mass times acceleration, or rearranged, acceleration equals force divided by mass. For the rocket, the net force at any instant is thrust minus weight minus drag. So acceleration equals thrust minus weight minus drag, all divided by the current mass of the rocket. The mass changes with time because propellant is being burned. Once you know acceleration at a given instant, you can find how velocity and height change over that instant, velocity changes by acceleration multiplied by the time step, and height changes by velocity multiplied by the time step. Repeating this process for thousands of tiny time steps traces the full trajectory. We also know that during the coasting phase, mass is constant and T=0, which factors into the equation.

also note eq(1) assumes vertical flight, but in reality is a vector equation, and can be calculated for both vertical and horizontal components $a_x$ and $a_y$.