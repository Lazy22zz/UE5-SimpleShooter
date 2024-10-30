# This is project(NOTE)
# 1, Add Movement Function
```c++
void AShooterCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
	Super::SetupPlayerInputComponent(PlayerInputComponent);
	PlayerInputComponent -> BindAxis (TEXT("MoveForward"), this, &AShooterCharacter::MoveForward);
	PlayerInputComponent -> BindAxis (TEXT("LookUp"), this, &AShooterCharacter::LookUp);
	PlayerInputComponent -> BindAxis(TEXT("MoveRight"), this, &AShooterCharacter::MoveRight);
	PlayerInputComponent -> BindAxis(TEXT("LookRight"), this, &AShooterCharacter::LookRight);
	PlayerInputComponent -> BindAction(TEXT("Jump"), EInputEvent::IE_Pressed, this, &AShooterCharacter::Jump);
}

void AShooterCharacter::MoveForward(float AxisValue)
{
	AddMovementInput(GetActorForwardVector() * AxisValue);
}

void AShooterCharacter::LookUp(float AxisValue)
{
	AddControllerPitchInput(AxisValue);
}

void AShooterCharacter::MoveRight(float AxisValue)
{
	AddMovementInput(GetActorRightVector() * AxisValue);
}

void AShooterCharacter::LookRight(float AxisValue)
{
	AddControllerYawInput(AxisValue);
}

```
- Actually, we can use class relationship to avoid some duplicate functions
  ```c++
  PlayerInputComponent->BindAxis(TEXT("LookUp"), this, &APawn::AddControllerPitchInput);
  PlayerInputComponent->BindAxis(TEXT("LookRight"), this, &APawn::AddControllerYawInput);
  ```
# 2，creating the controller aiming
- For Framerates and Axes
- Mouse : 30 FPS: 10, 10, 10
- Mouse : 60 FPS: 5, 5, 5, 5, 5, 5
- Controller : 30 FPS: 1, 1, 1
- Controller : 60 FPS: 1,1,1,1,1,1
- **SOLUTION**: 
```c++
// three directions: Roll, Pitch, Yaw, replace by "___"
AddController___Input(AxisValue * Rate * GetWorld()->GetDeltaSeconds() )
```
# 3, Adding Camera and Spring Arm
- Socket can enbale the rotate the springarm, Camera Settings -> Use Pawn Controller Rotate enables camera rotate by pawn movement
# 4, Add Animation
- Mesh, Animation is decided by the Skeletal.
