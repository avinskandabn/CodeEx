import { createSlice, PayloadAction } from '@reduxjs/toolkit';

export type StepKey = 'project' | 'source' | 'review';

interface StepperState {
  completedSteps: Record<StepKey, boolean>;
}

const initialState: StepperState = {
  completedSteps: {
    project: false,
    source: false,
    review: false,
  },
};

const stepperSlice = createSlice({
  name: 'stepper',
  initialState,
  reducers: {
    completeStep(state, action: PayloadAction<StepKey>) {
      state.completedSteps[action.payload] = true;
    },
    resetSteps(state) {
      state.completedSteps = initialState.completedSteps;
    },
  },
});

export const { completeStep, resetSteps } = stepperSlice.actions;
export default stepperSlice.reducer;
