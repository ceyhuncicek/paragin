<template>
  <div class="page">
    <Modal title="Add new correction round">
      <template #content>
        <Box title="Correction round settings">
          <div class="correction-round-settings">
            <Table>
              <TableBody>
                <TableRow class="row">
                  <TableData>Anonymous correction round</TableData>
                  <TableData>
                    <RadioInput
                      v-model="settings.anonymousCorrection"
                      :value="'no'"
                      label="No" />
                    <RadioInput
                      v-model="settings.anonymousCorrection"
                      :value="'yes'"
                      label="Yes" />
                  </TableData>
                </TableRow>
                <TableRow class="row">
                  <TableData>
                    Show scores and feedback from previous correction rounds
                  </TableData>
                  <TableData>
                    <RadioInput
                      v-model="settings.showPreviousScores"
                      :value="'no'"
                      label="No" />
                    <RadioInput
                      v-model="settings.showPreviousScores"
                      :value="'yes'"
                      label="Yes" />
                  </TableData>
                </TableRow>
                <TableRow class="row">
                  <TableData>
                    Previous correction rounds must be completed before this one
                    can start
                  </TableData>
                  <TableData>
                    <RadioInput
                      v-model="settings.previousRoundsMustBeCompleted"
                      :value="'no'"
                      label="No" />
                    <RadioInput
                      v-model="settings.previousRoundsMustBeCompleted"
                      :value="'yes'"
                      label="Yes" />
                  </TableData>
                </TableRow>
                <TableRow class="row">
                  <TableData>
                    After checking, the score and feedback can be edited
                  </TableData>
                  <TableData>
                    <RadioInput
                      v-model="settings.afterCheckingScoreCanBeEdited"
                      :value="'no'"
                      label="No" />
                    <RadioInput
                      v-model="settings.afterCheckingScoreCanBeEdited"
                      :value="'yes'"
                      label="Yes" />
                  </TableData>
                </TableRow>
                <TableRow class="row">
                  <TableData>
                    The result and grade will be updated based on this
                    correction round
                  </TableData>
                  <TableData>
                    <RadioInput
                      v-model="settings.afterCheckingGradeCanBeEdited"
                      :value="'no'"
                      label="No" />
                    <RadioInput
                      v-model="settings.afterCheckingGradeCanBeEdited"
                      :value="'yes'"
                      label="Yes" />
                  </TableData>
                </TableRow>
                <TableRow class="row">
                  <TableData>
                    Deadline, the number of days within which the result has to
                    be checked after submission
                  </TableData>
                  <TableData>
                    <div class="deadline-settings">
                      <div class="deadline-settings__slider">
                        <input
                          v-model="settings.deadline"
                          type="range"
                          min="0" />
                        <img
                          class="deadline-settings__icon"
                          src="/star-of-life-solid.svg" />
                      </div>
                      <input
                        type="number"
                        class="deadline-settings__input"
                        v-model="settings.deadline" />
                    </div>
                  </TableData>
                </TableRow>
              </TableBody>
            </Table>
          </div>
        </Box>
      </template>
      <template #secondaryButton>
        <Button variant="outlined" borderRadius="1x">Cancel</Button>
      </template>
      <template #primaryButton>
        <Button variant="contained" color="danger" borderRadius="1x">
          <i class="fas fa-exclamation-triangle"></i>
          Save this correction round
        </Button>
      </template>
    </Modal>
  </div>
</template>

<script>
import TableData from '../components/tables/atoms/TableData';
import TableRow from '../components/tables/atoms/TableRow';
import Box from '../components/boxes/molecules/Box';
import Button from '../components/forms/atoms/Button';
import Modal from '../components/modals/molecules/Modal';
import Table from '../components/tables/molecules/Table';
import TableBody from '../components/tables/atoms/TableBody';
import TableHeading from '../components/tables/atoms/TableHeading';
import TableHeader from '../components/tables/atoms/TableHeader';
import RadioInput from '../components/forms/molecules/RadioInput';

export default {
  name: 'IndexPage',
  components: {
    Modal,
    Button,
    Box,
    Table,
    TableHeader,
    TableHeading,
    TableBody,
    TableRow,
    TableData,
    RadioInput,
  },
  data() {
    return {
      settings: {
        anonymousCorrection: 'yes',
        showPreviousScores: 'yes',
        previousRoundsMustBeCompleted: 'yes',
        afterCheckingScoreCanBeEdited: 'yes',
        afterCheckingGradeCanBeEdited: 'yes',
        deadline: 7,
      },
    };
  },
};
</script>
<style>
:root {
  font-family: Arial, Helvetica, sans-serif;
  --main-color: #66aa11;
  --general-error: #cf191e;
  --text-title: #4a4a4a;
  --link-color: #3273f6;
  --white: #ffffff;
  --box-color: #fafafa;
  --box-zebra-inside: #f1f1f1;
  --box-border-outer: #ececec;
  --box-outer: #f1f1f1;
  --box-slider-line: #e1e1e1;
  --box-slider: #696969;
}

body {
  background-color: rgba(0, 0, 0, 0.7);
}
</style>

<style scoped>
.page {
  margin: 32px;
}

.correction-round-settings {
  color: black;
  font-weight: 400;
  font-size: 12px;
  line-height: 14px;
}

.deadline-settings {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: flex-end;
}

.deadline-settings__slider {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-bottom: 10px;
}

.deadline-settings__slider input[type='range'] {
  -webkit-appearance: none;
  appearance: none;
  background: transparent;
  cursor: pointer;
  width: 82px;

  background: var(--box-slider-line);
  height: 2px;
}

.deadline-settings__slider input[type='range']::-webkit-slider-thumb {
  appearance: none;
  background-color: var(--box-slider);
  height: 12px;
  width: 12px;
  border-radius: 50%;
}

.deadline-settings__icon {
  width: 10px;
  height: 10px;
}

.deadline-settings__input {
  width: 98px;
}
</style>
