### Custom Controls Checklist

- Create cockpit equipment
  - Movable section of equipment is only connected to the rest of the aircraft at the Control Base.
  - Each Control Base has one or more Grips.
  - Grip X and Z scale must be 1.

- Control Base
  - Select closest preset.
  - Add RotationAxis and PositionAxis, if required, from XML file.
  - Set input parameters.
    - Min, Max: setter limits of the Control Base
    - Rotation Max: maximum rotation multiplied with the scale parameter
  - Each input can be a rotation (for RotationAxis controls) or translation (for PositionAxis controls).
    - The axis is defined as Vector3 and the output is the length projected onto this axis.
  - Rotation of grip parts is detected in Control Base local space.

- Grips
  - Change triggerPressed (digital input) to trigger (analog input) if required.
  - Unused buttons should be disabled on non-standard controls.
  - Add screen space controls in PosedGrip:
    - Vector3 screen[XYZ]\[Position/Rotation]AxisMap: allows the simulation VR inputs to the Control Base axis in the parameter name.
      - Click-drag in the direction of the value of the parameter to produce a positive input. E.g., `1,0,0` ==> drag to the right to increase the input.
      - On Control Base equipment, it attempts to transform the part in aircraft local space (not Grip or Control Base space).
    - Vector3 screenAxisSize: screen space distance to drag for min/max inputs.
    - Vector3 screenAxisDeadzone: screen space distance to drag before any input applies on the aircraft.
