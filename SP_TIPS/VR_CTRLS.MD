### Custom Controls Checklist

- Create cockpit equipment
  - Movable section of equipment is only connected to the rest of the aircraft at the Control Base.
  - Each Control Base has one or more Grips.

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
  - Add screen space controls in PosedGrip. The following are Vector3:
    - screen[XYZ]\[Position/Rotation]AxisMap: simulate VR inputs by click-dragging along this axis on the screen.
      - It appears to attempt transforming the part in aircraft local space (not Grip or Control Base space)
    - screenAxisSize: distance to drag for min/max inputs
    - screenAxisDeadzone