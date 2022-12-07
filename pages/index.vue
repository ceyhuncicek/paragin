<template>
  <div class="page">
    <Modal title="Add new correction round">
      <template #content>
        <Box class="settings-box" title="Correction round settings">
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
        <Box class="distribution-box" title="Correction distribution">
          <div class="distribution-box__text">
            Corrections should be assigned to:
          </div>
          <div class="distribution-box__selection">
            <div
              :style="{
                color: assigned === 'corrector' ? 'white' : 'black',
                backgroundColor:
                  assigned === 'corrector' ? '#3273f6' : 'transparent',
              }"
              class="selection"
              @click="assignTo('corrector')">
              One corrector
            </div>
            <div
              :style="{
                color: assigned === 'myself' ? 'white' : 'black',
                backgroundColor:
                  assigned === 'myself' ? '#3273f6' : 'transparent',
              }"
              class="selection"
              @click="assignTo('myself')">
              Assign to me
            </div>
          </div>
          <div class="distribution-box__info">
            <template v-if="assigned === 'myself'">
              Correction distribution is assigned to: Assigned to me. You don’t
              need to specify anything else.
            </template>
            <template v-else-if="selectedCorrectors.length > 0">
              Correction distribution is assigned to:
              <span class="info-section">
                <span
                  v-for="(corrector, i) in selectedCorrectors"
                  :key="i"
                  class="info-section__selected">
                  {{ corrector.name }},
                </span>
                . You don’t need to specify anything else.
              </span>
            </template>
            <template v-else>
              Please select a corrector from the list below in order to assign
              your correction distribution.
            </template>
          </div>
          <div v-if="assigned === 'corrector'" class="corrector-table">
            <Table>
              <TableHeading>
                <TableHeader>Name</TableHeader>
                <TableHeader>Role</TableHeader>
                <TableHeader>Gorup</TableHeader>
                <TableHeader></TableHeader>
              </TableHeading>
              <TableBody>
                <TableRow
                  v-for="(corrector, i) in selectedCorrectors.length > 0
                    ? selectedCorrectors
                    : correctorList"
                  :key="i">
                  <TableData>{{ corrector.name }}</TableData>
                  <TableData>{{ corrector.role }}</TableData>
                  <TableData>{{ corrector.group }}</TableData>
                  <TableData>
                    <Button @click="toggleSelectedCorrector(corrector)">
                      {{
                        isCorrectorSelected(corrector)
                          ? 'Remove'
                          : 'Select this corrector'
                      }}
                    </Button>
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
        <Button
          v-if="assigned === 'myself' || selectedCorrectors.length > 0"
          variant="contained"
          color="main"
          borderRadius="1x">
          Save this correction round
        </Button>
        <Button v-else variant="contained" color="danger" borderRadius="1x">
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
      assigned: 'corrector',
      correctorList: [
        {
          id: 1,
          name: 'Van den Endelagen, C 1',
          role: 'Test Coordinator',
          group: 'Paragin Medewerkers Group XAAS',
        },
        {
          id: 2,
          name: 'Van den Endelagen, C 2',
          role: 'Test Coordinator',
          group: 'Paragin Medewerkers Group XAAS',
        },
        {
          id: 3,
          name: 'Van den Endelagen, C 3',
          role: 'Test Coordinator',
          group: 'Paragin Medewerkers Group XAAS',
        },
        {
          id: 4,
          name: 'Van den Endelagen, C 4',
          role: 'Test Coordinator',
          group: 'Paragin Medewerkers Group XAAS',
        },
        {
          id: 5,
          name: 'Van den Endelagen, C 5',
          role: 'Test Coordinator',
          group: 'Paragin Medewerkers Group XAAS',
        },
        {
          id: 6,
          name: 'Van den Endelagen, C 6',
          role: 'Test Coordinator',
          group: 'Paragin Medewerkers Group XAAS',
        },
        {
          id: 7,
          name: 'Van den Endelagen, C 7',
          role: 'Test Coordinator',
          group: 'Paragin Medewerkers Group XAAS',
        },
        {
          id: 8,
          name: 'Van den Endelagen, C 8',
          role: 'Test Coordinator',
          group: 'Paragin Medewerkers Group XAAS',
        },
        {
          id: 9,
          name: 'Van den Endelagen, C 9',
          role: 'Test Coordinator',
          group: 'Paragin Medewerkers Group XAAS',
        },
        {
          id: 10,
          name: 'Van den Endelagen, C 10',
          role: 'Test Coordinator',
          group: 'Paragin Medewerkers Group XAAS',
        },
      ],
      selectedCorrectors: [],
    };
  },
  methods: {
    isCorrectorSelected(corrector) {
      return this.selectedCorrectors.some(
        (selectedCorrector) => selectedCorrector.id === corrector.id
      );
    },
    assignTo(assignment) {
      if (assignment === 'myself') {
        this.selectedCorrectors = [];
      }
      this.assigned = assignment;
    },
    toggleSelectedCorrector(corrector) {
      if (this.isCorrectorSelected(corrector)) {
        return (this.selectedCorrectors = this.selectedCorrectors.filter(
          (selectedCorrector) => {
            return selectedCorrector.id !== corrector.id;
          }
        ));
      }
      return this.selectedCorrectors.push(corrector);
    },
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

.settings-box {
  margin-bottom: 10px;
}

.distribution-box__text {
  color: black;
  font-size: 12px;
  margin-bottom: 10px;
}
.distribution-box__selection {
  height: 44px;
  background-color: var(--box-outer);
  display: flex;
  align-items: center;
}

.selection {
  cursor: pointer;
  color: white;
  font-weight: 400;
  font-size: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 28px;
  border-radius: 60px;
  background-color: #3273f6;
  width: 100%;
}

.corrector-table {
  color: black;
  font-weight: 400;
  font-size: 12px;
}

.distribution-box__info {
  color: black;
  font-size: 12px;
}

.info-section__selected {
  font-weight: 600;
}
</style>
